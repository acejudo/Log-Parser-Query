# Log-Parser-Query
Log Parser Query Examples

# Group by Machine , IpServer , Uriname 
logparser  "SELECT  c-ip As Machine, REVERSEDNS(c-ip) As ReverseDNS, s-ip as IpServer,   cs(Referer) as Uriname       COUNT(*) As Hits   into [nameLog].csv FROM [namelog].log  GROUP BY Machine , IpServer, Uriname ORDER BY Hits DESC" 
