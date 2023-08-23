# tshark

While Wireshark is great for initial diagnosis and exploring, the goal should be to close the tool as quickly as possible. Moving to a programmable solution is a priority. The solution is tshark, use it to extract fields that you identify during initial triage. 

## Extract DNS Query Names

```bash
tshark -r example.pcap -T fields -e dns.qry.name
```

## Extract Multiple Fields - Including Frame Number

```bash
tshark -r example.pcap -T fields -e frame.number -e dns.qry.name 
```
## Other Resources

- [a more complete cheatsheet](https://snippets.bentasker.co.uk/page-1909131238-TShark-Cheatsheet-BASH.html)

