Certainly! Here are the top 5 Application Insights queries (Kusto queries), with a description, usage tips, the value they provide, and a sample use case for each—formatted in Markdown for easy documentation or sharing.

---

# Top 5 Application Insights Queries

## 1. Track Failed Requests

**Query:**
```kusto
requests
| where success == false
| order by timestamp desc
```

**Description:**  
Lists all failed requests in your application, ordered by most recent.

**Usage Tips:**
- Filter further by operation name or response code to pinpoint specific issues.
- Combine with visualization for failure trends.

**Value:**  
Quickly identifies failing endpoints and their frequency, helping prioritize fixes.

**Sample Use Case:**  
A sudden spike in failed requests after a deployment can be tracked to the responsible API endpoints.

---

## 2. Analyze Top Slowest Dependencies

**Query:**
```kusto
dependencies
| order by duration desc
| take 10
```

**Description:**  
Shows the 10 slowest external dependencies (like SQL, HTTP, or storage).

**Usage Tips:**
- Filter by dependency type to focus on critical services (e.g., SQL).
- Investigate high-duration dependencies for performance bottlenecks.

**Value:**  
Helps to uncover external systems causing slowdowns and impacting user experience.

**Sample Use Case:**  
Identifying a database query that is significantly slower than others and optimizing it.

---

## 3. Count Unique Users

**Query:**
```kusto
customEvents
| summarize users=dcount(user_Id)
```

**Description:**  
Counts the number of distinct users who triggered custom events.

**Usage Tips:**
- Use this to monitor active user engagement over time.
- Combine with filters for specific events or time ranges.

**Value:**  
Provides a quick measure of your application's reach and activity.

**Sample Use Case:**  
Measuring weekly active users for a product dashboard.

---

## 4. Monitor Exception Trends

**Query:**
```kusto
exceptions
| summarize count() by bin(timestamp, 1h), type
| order by timestamp desc
```

**Description:**  
Displays the count of exceptions grouped by type and hour.

**Usage Tips:**
- Use bin sizes (e.g., `1h`, `1d`) that match your monitoring needs.
- Drill down into specific exception types for root cause analysis.

**Value:**  
Helps in spotting exception spikes, trends, and recurring error patterns.

**Sample Use Case:**  
Noticing a rise in "NullReferenceException" after a recent code release.

---

## 5. Identify Most Used Pages or Features

**Query:**
```kusto
pageViews
| summarize count() by name
| top 10 by count_
```

**Description:**  
Lists the top 10 most visited pages or features by usage count.

**Usage Tips:**
- Adjust `top 10` as needed for broader or narrower views.
- Cross-reference with session or user data for deeper insights.

**Value:**  
Reveals the most popular (or least used) parts of your application, guiding UX improvements.

**Sample Use Case:**  
Determining which product features to enhance based on user engagement.

---

> **Tip:**  
Use the [Application Insights Analytics portal](https://portal.azure.com/) for running these queries, visualizing results, and setting up alerts.

---

If you need more tailored queries or advanced tips for your specific scenario, let me know!
