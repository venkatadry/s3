# s3
s3

 Durability                         | S3 Standard  | S3 Intelligent-Tiering | S3 Standard-IA   | S3 One Zone-IA   | S3 Glacier       |
| ---------------------------------- | ------------ | ---------------------- | ---------------- | ---------------- | ---------------- |
| Availability                       | 100.00%      | 100.00%                | 100.00%          | 100.00%          | 100.00%          |
| Availability                       | 99.99%       | 99.90%                 | 99.90%           | 99.50%           | 99.99%           |
| Availability SLA                   | 99.90%       | 99%                    | 99%              | 99.90%           | 99.90%           |
| Availability Zones                 | ≥3           | ≥3                     | ≥3               | 1                | ≥3               |
| Storage Type                       | Object       | Object                 | Object           | Object           | Object           |
| Minimum capacity charge per object | N/A          | N/A                    | 128KB            | 128KB            | 40KB             |
| Minimum storage duration charge    | N/A          | 30 days                | 30 days          | 30 days          | 180 days         |
| Retrieval Fees                     | N/A          | N/A                    | per GB retrieved | per GB retrieved | per GB retrieved |
| First byte latency                 | milliseconds | milliseconds           | milliseconds     | milliseconds     | Minutes to Hours |
| Storage class                                 | Designed for                                                                                                           | Bucket type                  | Availability Zones | Min storage duration | Min billable object size | Monitoring and auto-tiering fees            | Retrieval fees    |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------------------- | ------------------ | -------------------- | ------------------------ | ------------------------------------------- | ----------------- |
| Standard                                      | Frequently accessed data (more than once a month) with milliseconds access                                             | General purpose              | ≥ 3                | \-                   | \-                       | \-                                          | \-                |
| Intelligent-Tiering                           | Data with changing or unknown access patterns                                                                          | General purpose              | ≥ 3                | \-                   | \-                       | Per-object fees apply for objects >= 128 KB | \-                |
| Standard-IA                                   | Infrequently accessed data (once a month) with milliseconds access                                                     | General purpose              | ≥ 3                | 30 days              | 128 KB                   | \-                                          | Per-GB fees apply |
| One Zone-IA                                   | Recreatable, infrequently accessed data (once a month) with milliseconds access                                        | General purpose or directory | 1                  | 30 days              | 128 KB                   | \-                                          | Per-GB fees apply |
| Glacier Instant Retrieval                     | Long-lived archive data accessed once a quarter with instant retrieval in milliseconds                                 | General purpose              | ≥ 3                | 90 days              | 128 KB                   | \-                                          | Per-GB fees apply |
| Glacier Flexible Retrieval (formerly Glacier) | Long-lived archive data accessed once a year with retrieval of minutes to hours                                        | General purpose              | ≥ 3                | 90 days              | \-                       | \-                                          | Per-GB fees apply |
| Glacier Deep Archive                          | Long-lived archive data accessed less than once a year with retrieval of hours                                         | General purpose              | ≥ 3                | 180 days             | \-                       | \-                                          | Per-GB fees apply |
| Reduced redundancy                            | Noncritical, frequently accessed data with milliseconds access (not recommended as S3 Standard is more cost effective) | General purpose              | ≥ 3                | \-                   | \-                       | \-                                          | Per-GB fees apply |
Understanding AWS S3 Storage Classes
**AWS Glacier:** This storage class is ideal for long-term archival data. Objects in Glacier must be retained for a minimum of 90 days. After 90 days, you can retrieve the data, but keep in mind the costs associated with retrievals and the time it takes.

**AWS Glacier Deep Archive:** If you need to store data for longer periods, the Glacier Deep Archive is a cost-effective option. However, it has a minimum retention period of 180 days, making it suitable for compliance or long-term storage.

Amazon S3 Storage Classes – Use Cases
Amazon S3 Storage Classes – Use Cases
1. **S3 Standard**  
   Frequently accessed data (e.g., live websites, dynamic content, big data analytics).

2. **S3 Intelligent-Tiering**  
   Data with unpredictable or changing access patterns (e.g., user-generated content, analytics datasets).

3. **S3 Standard-IA (Infrequent Access)**  
   Long-lived, less frequently accessed data (e.g., backups, disaster recovery files).

4. **S3 One Zone-IA**  
   Infrequently accessed, non-critical data (e.g., secondary backups, easily recreatable data).

5. **S3 Glacier**  
   Long-term archival with rare retrievals (e.g., compliance archives, medical records, financial logs).

6. **S3 Glacier Deep Archive**  
   Rarely accessed data with long-term retention (e.g., regulatory archives, 7+ year compliance storage).

**Performance:** Standard > Intelligent-Tiering > Standard-IA > One Zone-IA > Glacier > Deep Archive  
**Cost:** Deep Archive < Glacier < One Zone-IA < Standard-IA < Intelligent-Tiering < Standard  
**Choose based on:** Access frequency, retrieval time needs, and durability requirements

