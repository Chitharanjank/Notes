### 6. S3 Gateway Endpoint
- **S3 Gateway Endpoint** allows **private** access to S3 from within a **VPC** without using the public internet.
- Eliminates the need for a **NAT Gateway or Internet Gateway**.
- **Use Cases:**
  - Ensures **secure and private** access to S3.
  - Reduces **data transfer costs**.
  - Improves **network performance**.
- **How to Create:**
  1. Go to **VPC Console** → **Endpoints** → **Create Endpoint**.
  2. Select **AWS Service** and choose **com.amazonaws.<region>.s3**.
  3. Choose the **VPC** and **Route Table** to associate it with.
  4. Select **Policy** (Full Access or Custom).
  5. Create the Endpoint and update Route Tables if needed.

---

### Architecture
 ![My Image](/Images/s3-endpoint.jpg) 