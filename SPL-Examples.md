
# 📘 Common SPL Scripts for Splunk

This document provides a collection of useful SPL (Search Processing Language) scripts commonly used with Splunk for log analysis, troubleshooting, and performance monitoring.

## 📌 Notes

- Replace `index=web_logs` with your actual index if needed.
- Use `earliest` and `latest` to control time range.
- Pipe (`|`) is used to chain commands, similar to shell scripting.
- These queries can be run from Splunk Web, REST API, or SDKs.
- SPL is powerful for building dashboards, alerts, and operational intelligence views.

---

## 1. 🔎 Basic Error Search

Search for HTTP 500 errors in the last 24 hours:

```spl
index=web_logs status=500 earliest=-24h@h latest=now
```

> This finds all logs in the `web_logs` index with status code `500` (internal server error) within the last 24 hours.

---

## 2. 📊 Top Talkers by IP

Show top 10 IPs by request volume:

```spl
index=web_logs | top limit=10 client_ip
```

> This returns the 10 most active client IPs based on the number of events.

---

## 3. 📈 Event Count Over Time

Count events per minute for the last hour (ideal for visualizing trends):

```spl
index=web_logs earliest=-60m@m latest=now
| timechart span=1m count
```

> This builds a time-series chart showing the number of events every minute.

---

## 4. 🛠️ Average Response Time per URL

Identify which endpoints are slowest on average:

```spl
index=web_logs
| stats avg(response_time) as avg_response by uri_path
| sort - avg_response
```

> This calculates and ranks the average response time for each URI path.

---

