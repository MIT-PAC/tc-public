## Upload Data to BBN's bits server

`ssh -L 9999:files.tc.bbn.com:22 mgordon@gw.tc.bbn.com`

`scp -P 9999 avro-files mgordon@localhost:/files/datasets/clearscope`

## Log on to VM at BBN

`ssh mgordon@gw.tc.bbn.com`

`ssh  clearscope@ta1-clearscope-build-vm.tc.bbn.com` (password mitaarno)

