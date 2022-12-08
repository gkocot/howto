### Example queries in the Application Insights Logs
```code
traces
| where timestamp > ago(1h) 
| where customDimensions contains "videogateway"
| where message contains "VideoGateway"

union traces, exceptions
| where timestamp > ago(1h)
| where customDimensions.resourceName contains "Signaling"
| order by timestamp asc

let gwId = "000000000000000000000000000000150764";
let filename = "videogateway";
traces
//| where timestamp >= todatetime('2021-04-21T19:00:00Z')
//| where timestamp >= todatetime('2021-04-21T19:00:00Z')
| where customDimensions.resourceName == "GatewaysLogsIngestionFunction" 
| where customDimensions.deviceId == gwId
| where customDimensions.logFileName startswith filename
//| project filename = tostring(customDimensions.logFileName) , line = toint(customDimensions.lineNumber) , time_log = todatetime(customDimensions.logTime), message = tostring(message), timestamp
| extend video_log_time = todatetime(extract('\"time\":(.+\\d{6})Z,',1,message))
//| extend msg = extract('\"msg\":\"(.+)\",',1,message)
//| order by filename asc, line asc
//| where video_log_time >= todatetime('2021-04-21T18:58:00Z')
//| where msg contains "failed"
| project video_log_time, message = tostring(message)
//| where (video_log_time >= datetime(2021-04-21T02:46:03Z) and video_log_time <= datetime(2021-04-21T02:47:25Z)) or (video_log_time >= datetime(2021-04-21T20:00:06Z) and video_log_time <= datetime(2021-04-21T20:00:17Z))
| where (video_log_time >= datetime(2021-04-21T00:00:00Z) and video_log_time <= datetime(2021-04-22T00:00:00Z))
| where (message contains "error" or message contains "failed") and not (message contains "\"error\": null")
| order by video_log_time asc

let gwId = "000000000000000000000000000000150764";
let filename = "videogateway";
traces
//| where timestamp >= todatetime('2021-04-21T19:00:00Z')
//| where timestamp >= todatetime('2021-04-21T19:00:00Z')
| where customDimensions.resourceName == "GatewaysLogsIngestionFunction" 
| where customDimensions.deviceId == gwId
| where customDimensions.logFileName startswith filename
//| project filename = tostring(customDimensions.logFileName) , line = toint(customDimensions.lineNumber) , time_log = todatetime(customDimensions.logTime), message = tostring(message), timestamp
| extend video_log_time = todatetime(extract('\"time\":(.+\\d{6})Z,',1,message))
//| extend msg = extract('\"msg\":\"(.+)\",',1,message)
//| order by filename asc, line asc
//| where video_log_time >= todatetime('2021-04-21T18:58:00Z')
//| where msg contains "failed"
| project video_log_time, message = tostring(message)
| where (video_log_time >= datetime(2021-04-21T01:45:03Z) and video_log_time <= datetime(2021-04-21T01:48:25Z)) or (video_log_time >= datetime(2021-04-21T18:59:06Z) and video_log_time <= datetime(2021-04-21T19:01:17Z))
//| where (video_log_time >= datetime(2021-04-21T00:00:00Z) and video_log_time <= datetime(2021-04-22T00:00:00Z))
| where (message contains "error" or message contains "failed") and not (message contains "\"error\": null")
| order by video_log_time asc


traces
| where customDimensions.resourceName == "GatewaysLogsIngestionFunction" 
| where customDimensions.logFileName startswith "azurebridge"
| extend log_time = todatetime(customDimensions.logTime)
| where log_time >= datetime(2021-04-21T01:45:00Z) and log_time <= datetime(2021-04-21T01:48:00Z) or (log_time >= datetime(2021-04-21T18:59:00Z) and log_time <= datetime(2021-04-21T19:01:00Z))
| project log_time, message
| order by log_time asc

traces
| where customDimensions.resourceName == "GatewaysLogsIngestionFunction" 
| where customDimensions.logFileName startswith "s2"
| where message startswith "Apr 21"
| extend log_time = todatetime(strcat('2021-04-21T', extract('(\\d{2}:\\d{2}:\\d{2})', 1, message), 'Z'))
| where log_time >= datetime(2021-04-21T01:40:00Z) and log_time <= datetime(2021-04-21T01:48:00Z) or (log_time >= datetime(2021-04-21T18:55:00Z) and log_time <= datetime(2021-04-21T19:01:00Z))
| project log_time, message
| order by log_time asc
```