# Questions and Answers from TA2 Teams

## Provenance Tags

### Question

For the new data in this engagement, in order to build a graph of
connected provenance tags, do we only look into two cases:

1. the TAG_OP_UNION type (use getTagIDs()), which has a list of
previous provTagIDs and

2. getPrevTagId() (this is a TAG_OP_SEQUENCE in previous engagement), right? 
 
What else could help reconstruct the information flow edges among provNodes?

### Answer

For engagement 2, we support CDM17, and our recent examples are all
CDM17.  It seems like you understand our provenance encoding in CDM17.
Yes, provenance history is encoded in the ProvenanceTagNODE as tagIds
(with TAG_OP_UNION) and prevTagId.  They will never be both defined. 

These fields will allow you to create the provenance history and
construction your information flow edges.  Please let me know if you
want more information, or if anything else would be helpful. 

## Orphaned ProvenanceTagNodes

### Question

When building the provenance graph using the UNION and prevTagId
cases, by adding edges between each UNION tagID --> tagID and the
prevTagID --> tagID, we still found a lot of tagIDs that has 0 edge
connections (e.g., example the tags, 000035, 00003a, 000017 in the
basicOps dataset). 
 
Are we missing some other cases here that could build the flow edges?
Or there are some explanations for the orphan tagIDs. 

### Answer

You should expect a lot of tags with no ancestors.  This is because 1)
programs compute on homogenous data, and thus we see few union tags,
and 2) previous tags are created when data flows through multiple
sources and sinks, which is not the common case for data. 

## Ignore Orphaned Tags?

### Question

Then we could simply ignore those tags without ancestors, right? Those
tags mean the data is generated without further computation or flow.  

### Answer

That is up to you.  But I think you should not ignore them.  For
example, if an application reads a file that was written by a
process we do not track, then the file data read will not have a
previous tag.  Then if this data is written to the network, you will
probably want to record that action.

At the network sink, the tag reported on the data written will be the
tag denoting the file read information.  The NetFlowObject on the event
corresponding to the network sink will provide the connection details
(local and destination address / port).  That is just one example.
Files are another.

## NetFlowObjects and ProvenanceTagNodes

### Question

I further checked some of the netflowObjects in the BasicOps dataset, and found 3 out of 7 are not matched in the netflowObject of any ProvenanceNode. 
 
Not sure what is the criteria that you choose to encode in the ProvenanceNode.  I have put the result in the attachment. My matching result should have no missing cases, basically, I stored all the netflowObjects in one scan of all the records and matched against the ProvenanceNode in the second scan.
 
Also, for the NetflowObject, SrcSinkObject, FileObject, how could we know if the Object is a Source or a Sink. Based on the system call type or the relevant event types? 

### Answer

It is not a requirement that a NetFlowObject be used in a ProvenanceNode.  NetFlowObjects (FileObject, SrcSinkObject, etc.) are also referenced in the predicateObject field of Events.  For example, look at NetFlowObject 00000000000000000000000000007dc3.  This NetFlowObject is referenced in this event (a network sendto):

```
{
  "datum" : {
    "com.bbn.tc.schema.avro.Event" : {
      "uuid" : "97F3B058-814A-B62A-0786-84D139FB3F37",
      "sequence" : 93,
      "type" : "EVENT_SENDTO",
      "threadId" : 175,
      "subject" : "00000000-0000-0000-0000-000000007D01",
      "predicateObject" : {
        "com.bbn.tc.schema.avro.UUID" : "00000000-0000-0000-0000-000000007DC3"
      },
      "predicateObjectPath" : null,
      "predicateObject2" : null,
      "predicateObject2Path" : null,
      "timestampNanos" : 1489673909433000000,
      "name" : {
        "string" : "int libcore.io.Posix.sendto(java.io.FileDescriptor fd, byte[] bytes, int byteOffset, int byteCount, int flags, java.net.InetAddress inetAddress, int port) [line: 626]"
      },
      "parameters" : { ...
```

Referencing the NetFlowObject in the event informs you of the source ip / port and destination ip/port of the network communication.  Remember that we report the tag on a sink at the point "before" data enters the sink.  So, the provenance tag node associated with data written by a network write will not have the information from the network sink.  You must look at the netflow object associated with the predicate object of the network write event.

NetFlowObjects, SrcSinkObjects, and FileObjects can be used in both sources and sinks.  You will have to look at where the object is referenced in the predicate object field of an event to determine whether the event is a source or sink.  In the example above, the netflow object is referenced in an EVENT_SENDTO, so it is a sink.

## Strings in CDM Output
 
### Question

Today’s thought is about ‘bytes’ fields that represent strings in the CDM. When we dump the cdm, strings are often  represented as a long series of digits with 8 digits per byte. E.G., in the binder analysis walkthrough, ‘wifi’ is represented as ‘00000077000000690000006600000069’. Yet, there are also instances where the leading zeroes appear to be suppressed (e.g., ‘77696669’). It is frequently useful to view these strings as human-readable text, so we have written various decoders for the bytes strings. Do you know if this variation is a product of the way CS records the strings in the CDM-format data, or of the way it’s being deserialized? If it’s post-CS, I can try to hunt it down downstream.

### Answer

Without seeing examples, I'm pretty sure that the encoding discrepancy stems from the data type of the value being reported.  If the value is a java String data type (or C/++ char*), it will be encoded as UTF32BE, as specified upon in the CDM17 spec.  

However, no attempt is made by CS to try to encode general data of types like byte[] and char*.  If an ascii sequence is written to the network, for example, the data type for the buffer is byte[], and CS reports the raw bytes value (without attempting to determine the underlying type of what is written to the network).  So, if you are trying to read strings in a consistent manner from these general types, you are going to have to do a best effort decoding on byte[] values.  
 
 
### Question

Going forward, we would like to be able to consistently identify when each decoding type should be applied, and when the encoded values aren’t actually strings. There is a data type field in the CDM that isn’t set in the ADUPS data; not sure if you’re intending to set it for CDM17 data. For nodes where the called function prototype is available, it should be possible to determine which bytestreams should be strings and which shouldn’t. In a perfect world it would be nice to have the strings start out as text instead of ASCII codes, but that may be infeasible at the T1 layer. I’m all for an efficient solution at the T1 layer, as long as it’s consistent so we can write a tool or adapter without too much pain.

### Answer

You will not be able to consistently identify the encoding type for general data types like byte[] or void*.  TA1s cannot do that without *significant* cost.  Again, you will have to best-effort decode.  

The ValueDataType field of Value of our CDM17 ​captures should be set in all Value records.  I just verified that our CDM17 data linked above has the ValueDataType field set for all Value records.  Please let me know if this is not the case.

The Adups data represented a time when we had incomplete support for CDM16.  You *should not* take the adups data as representative of our Engagement 2 CDM output.

To reiterate, string types like java's String and C/C++'s char* will be classified as VALUE_DATA_TYPE_CHAR.  General types like void* and byte[], will be reported as the raw bytes seen at the call (with no encoding).
