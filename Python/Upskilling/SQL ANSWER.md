### ANSI SQL Using MySQL Exercises Answers

Prepared by : AFIFA A

College : Saveetha Engineering College

Dept&Yr : III Yr B.E( CSE )


## 1. User Upcoming Events

```sql
SELECT u.full_name, e.title, e.start_date
FROM Users u
JOIN Registrations r ON u.user_id = r.user_id
JOIN Events e ON r.event_id = e.event_id
WHERE e.status = 'upcoming';
```

## 2. Top Rated Events

```sql
SELECT event_id, AVG(rating) AS avg_rating
FROM Feedback
GROUP BY event_id
ORDER BY avg_rating DESC;
```

## 3. Inactive Users

```sql
SELECT *
FROM Users
WHERE user_id NOT IN (
SELECT user_id FROM Registrations
);
```

## 4. Peak Session Hours

```sql
SELECT event_id, COUNT(*) AS total_sessions
FROM Sessions
WHERE HOUR(start_time) BETWEEN 10 AND 12
GROUP BY event_id;
```

## 5. Most Active Cities

```sql
SELECT city, COUNT(*) AS total_users
FROM Users
GROUP BY city
ORDER BY total_users DESC
LIMIT 5;
```

## 6. Event Resource Summary

```sql
SELECT event_id, resource_type, COUNT(*) AS total
FROM Resources
GROUP BY event_id, resource_type;
```

## 7. Low Feedback Alerts

```sql
SELECT user_id, comments
FROM Feedback
WHERE rating < 3;
```

## 8. Sessions per Upcoming Event

```sql
SELECT e.title, COUNT(s.session_id) AS total_sessions
FROM Events e
JOIN Sessions s ON e.event_id = s.event_id
WHERE e.status = 'upcoming'
GROUP BY e.title;
```

## 9. Organizer Event Summary

```sql
SELECT organizer_id, status, COUNT(*) AS total_events
FROM Events
GROUP BY organizer_id, status;
```

## 10. Feedback Gap

```sql
SELECT event_id
FROM Registrations
WHERE event_id NOT IN (
SELECT event_id FROM Feedback
);
```

## 11. Daily New User Count

```sql
SELECT registration_date, COUNT(*) AS total_users
FROM Users
GROUP BY registration_date;
```

## 12. Event with Maximum Sessions

```sql
SELECT event_id, COUNT(*) AS total_sessions
FROM Sessions
GROUP BY event_id
ORDER BY total_sessions DESC
LIMIT 1;
```

## 13. Average Rating per City

```sql
SELECT e.city, AVG(f.rating) AS avg_rating
FROM Events e
JOIN Feedback f ON e.event_id = f.event_id
GROUP BY e.city;
```

## 14. Most Registered Events

```sql
SELECT event_id, COUNT(*) AS total_registrations
FROM Registrations
GROUP BY event_id
ORDER BY total_registrations DESC
LIMIT 3;
```

## 15. Event Session Time Conflict

```sql
SELECT *
FROM Sessions s1, Sessions s2
WHERE s1.event_id = s2.event_id
AND s1.session_id <> s2.session_id
AND s1.start_time < s2.end_time
AND s1.end_time > s2.start_time;
```

## 16. Unregistered Active Users

```sql
SELECT *
FROM Users
WHERE user_id NOT IN (
SELECT user_id FROM Registrations
);
```

## 17. Multi-Session Speakers

```sql
SELECT speaker_name, COUNT(*) AS total_sessions
FROM Sessions
GROUP BY speaker_name
HAVING COUNT(*) > 1;
```

## 18. Resource Availability Check

```sql
SELECT *
FROM Events
WHERE event_id NOT IN (
SELECT event_id FROM Resources
);
```

## 19. Completed Events with Feedback Summary

```sql
SELECT e.title, COUNT(r.registration_id), AVG(f.rating)
FROM Events e
JOIN Registrations r ON e.event_id = r.event_id
JOIN Feedback f ON e.event_id = f.event_id
WHERE e.status = 'completed'
GROUP BY e.title;
```

## 20. User Engagement Index

```sql
SELECT u.full_name,
COUNT(r.event_id) AS events,
COUNT(f.feedback_id) AS feedbacks
FROM Users u
LEFT JOIN Registrations r ON u.user_id = r.user_id
LEFT JOIN Feedback f ON u.user_id = f.user_id
GROUP BY u.full_name;
```

## 21. Top Feedback Providers

```sql
SELECT user_id, COUNT(*) AS total_feedbacks
FROM Feedback
GROUP BY user_id
ORDER BY total_feedbacks DESC
LIMIT 5;
```

## 22. Duplicate Registrations Check

```sql
SELECT user_id, event_id, COUNT(*) AS total
FROM Registrations
GROUP BY user_id, event_id
HAVING COUNT(*) > 1;
```

## 23. Registration Trends

```sql
SELECT MONTH(registration_date) AS month,
COUNT(*) AS total
FROM Registrations
GROUP BY MONTH(registration_date);
```

## 24. Average Session Duration per Event

```sql
SELECT event_id,
AVG(TIMESTAMPDIFF(MINUTE,start_time,end_time)) AS avg_duration
FROM Sessions
GROUP BY event_id;
```

## 25. Events Without Sessions

```sql
SELECT *
FROM Events
WHERE event_id NOT IN (
SELECT event_id FROM Sessions
);
```
