# Log-Parser-Query
Log Parser Query Examples

###  Group by Machine , IpServer , Uriname 
```
logparser  "SELECT  c-ip As Machine, REVERSEDNS(c-ip) As ReverseDNS, s-ip as IpServer,   cs(Referer) as Uriname,       COUNT(*) As Hits   into [nameLog].csv FROM [namelog].log  GROUP BY Machine , IpServer, Uriname ORDER BY Hits DESC" 
```

###  Group by Machine , IpServer , Uriname. Several logs
```
logparser  "SELECT  c-ip As Machine, REVERSEDNS(c-ip) As ReverseDNS , s-ip as IpServer,  cs(Referer) as Uriname,     COUNT(*) As Hits   into 1611.csv FROM u_ex16110*.log  GROUP BY Machine , IpServer, Uriname ORDER BY Hits DESC"  
```

###  Group by Machine , IpServer , Uriname. Several logs Select With date
logparser  "SELECT  c-ip As Machine, REVERSEDNS(c-ip) As ReverseDNS , s-ip as IpServer,  cs(Referer) as Uriname,     COUNT(*) As Hits   into 1611.csv FROM u_ex16110*.log  where  TO_TIMESTAMP(date, time) > TIMESTAMP('2016-11-03 17:30', 'yyyy-MM-dd HH:mm')   GROUP BY Machine , IpServer, Uriname ORDER BY Hits DESC"  

###  Response 500 Several Logs
```
logparser  "SELECT  date as Date,c-ip As Machine,    REVERSEDNS(c-ip) As ReverseDNS  , s-ip as IpServer,  cs(Referer) as Uriname , cs-uri-stem as UrlSend, cs-uri-query as Query into 1611.csv FROM u_ex16110*.log WHERE sc-status=500"  
```
###  Find the Slowest 25 URLs 
```
logparser  "SELECT TOP 25   cs-uri-stem as URL,   MAX(time-taken) As Max, MIN(time-taken) As Min,   Avg(time-taken) As Average           into Slowest1611.csv FROM u_ex16110*.log GROUP BY URL  ORDER By Average DESC" 
```
###  List Status Code
```
logparser " SELECT TOP 25   STRCAT(TO_STRING(sc-status),  STRCAT('.', TO_STRING(sc-substatus))) As Status,   COUNT(*) AS Hits     into Status.csv  FROM u_ex16110*.log  GROUP BY Status   ORDER BY Status ASC "
```
###  Chart Status Code (Need install https://www.microsoft.com/en-us/download/details.aspx?id=22276)
```
logparser "SELECT sc-status AS Status,COUNT(*) AS Hits INTO HITS.gif  FROM u_ex16110*.log GROUP BY Status ORDER BY Status" -i:w3c -o:CHART -chartType:PieExploded3D -chartTitle:""
```

###   Win32 Error Codes
```
logparser " SELECT   sc-win32-status As Win32-Status,WIN32_ERROR_DESCRIPTION(sc-win32-status) as Description,   COUNT(*) AS Hits      into ErrorCode.csv  FROM u_ex16110*.log WHERE Win32-Status<>0  GROUP BY Win32-Status  ORDER BY Win32-Status ASC" 
```
