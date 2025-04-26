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

Understanding AWS S3 Storage Classes
**AWS Glacier:** This storage class is ideal for long-term archival data. Objects in Glacier must be retained for a minimum of 90 days. After 90 days, you can retrieve the data, but keep in mind the costs associated with retrievals and the time it takes.

**AWS Glacier Deep Archive:** If you need to store data for longer periods, the Glacier Deep Archive is a cost-effective option. However, it has a minimum retention period of 180 days, making it suitable for compliance or long-term storage.

Amazon S3 Storage Classes – Use Cases
Amazon S3 Storage Classes – Use Cases
1.	**S3 Standard**
o	Frequently accessed data (e.g., live websites, dynamic content, big data analytics).
2.	**S3 Intelligent-Tiering**
o	Data with unpredictable or changing access patterns (e.g., user-generated content, analytics datasets).
3.	**S3 Standard-IA (Infrequent Access)**
o	Long-lived, less frequently accessed data (e.g., backups, disaster recovery files).
4.	**S3 One Zone-IA**
o	Infrequently accessed, non-critical data (e.g., secondary backups, easily recreatable data).
5.	**S3 Glacier**
o	Long-term archival with rare retrievals (e.g., compliance archives, medical records, financial logs).
6.	**S3 Glacier Deep Archive**
o	Rarely accessed data with long-term retention (e.g., regulatory archives, 7+ year compliance storage)

**Performance:** Standard > Intelligent-Tiering > Standard-IA > One Zone-IA > Glacier > Deep Archive.
**Cost:** Deep Archive < Glacier < One Zone-IA < Standard-IA < Intelligent-Tiering < Standard.
**Choose based on:** Access frequency, retrieval time needs, and durability requirements.
