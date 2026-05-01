# 📘 AWS S3 Versioning Demo

## 🔹 Step 1: Create S3 Bucket

At first, I logged into the AWS Console Dashboard and went to S3 (Simple Storage Service).  
Then I selected **Create Bucket**.

- Gave the bucket a unique name: `my-versioning-demo-bucket-s3`
- Kept all other settings as default (anyone can customize if needed)

Finally:
- Clicked on **Create Bucket**
- Selected the created bucket from the list

---

## 📸 Screenshots

![Step 1](s3-versioning-img/1.png)  
![Step 2](s3-versioning-img/2.png)  
![Step 3](s3-versioning-img/3.png)  
![Step 4](s3-versioning-img/4.png)

## 🔹 Step 2: Enable Versioning

After creating the bucket, I opened the bucket and went to the **Properties** tab.

- Scrolled down to **Bucket Versioning**
- Clicked on **Edit**
- Selected **Enable**
- Clicked on **Save Changes**

👉 Now versioning is enabled for this bucket

---

## 📸 Screenshots

![Step 5](s3-versioning-img/5.png)  
![Step 6](s3-versioning-img/6.png)  
![Step 7](s3-versioning-img/7.png)

## 🔹 Step 3: Upload First File (Version 1)

After enabling versioning, I went to the created bucket and clicked on **Upload**.

- Clicked on **Add files**
- Selected `1.txt` file
- Clicked on **Upload**

After successful upload:
- Opened `1.txt`
- The file content was:
Hello Version 1


👉 This is the first version of the file stored in S3 (Version 1)

---

## 📸 Screenshots

![Step 8](s3-versioning-img/8.png)  
![Step 9](s3-versioning-img/9.png)  
![Step 10](s3-versioning-img/10.png)  
![Step 11](s3-versioning-img/11.png)  
![Step 12](s3-versioning-img/12.png)  
![Step 13](s3-versioning-img/13.png)

## 🔹 Step 4: Modify File & Check Versions

Text file `1.txt` modify করে content change করা হলো:
Hello Version 2

Then go to bucket:

- Clicked on **Upload**
- Selected **Add files**
- Uploaded updated `1.txt`

After upload:
- Opened `1.txt`
- Verified upload success

Then I went to **Show versions**:

- Found **2 versions** of the file
- Each version had a different **Version ID**

Opened both versions:
- First version showed content: `Hello Version 1`
- Second version showed content: `Hello Version 2`

---

## 📸 Screenshots

![Step 14](s3-versioning-img/14.png)  
![Step 15](s3-versioning-img/15.png)  
![Step 16](s3-versioning-img/16.png)  
![Step 17](s3-versioning-img/17.png)  
![Step 18](s3-versioning-img/18.png)  
![Step 19](s3-versioning-img/19.png)  
![Step 20](s3-versioning-img/20.png)  
![Step 21](s3-versioning-img/21.png)  
![Step 22](s3-versioning-img/22.png)  
![Step 23](s3-versioning-img/23.png)  
![Step 24](s3-versioning-img/24.png)

## 🔹 Step 5: Re-upload Same File (Version 2 Check)

In this step, I uploaded the same `1.txt` file again to the S3 bucket.

- Went to the bucket
- Clicked on **Upload**
- Selected **Add files**
- Chose `1.txt` again
- Clicked on **Upload**

After successful upload:
- Opened `1.txt`
- Verified the file content in the bucket

---

## 📸 Screenshots

![Step 25](s3-versioning-img/25.png)  
![Step 26](s3-versioning-img/26.png)  
![Step 27](s3-versioning-img/27.png)  
![Step 28](s3-versioning-img/28.png)  
![Step 29](s3-versioning-img/29.png)

## 🔹 Step 6: Upload Modified File (Version 3)

In this step, I modified the `1.txt` file again and updated the content to:
Hello Version 3

Then I uploaded it to the S3 bucket:

- Went to the bucket
- Clicked on **Upload**
- Selected **Add files**
- Chose the updated `1.txt` file
- Clicked on **Upload**

After successful upload:
- Opened `1.txt`
- Verified the output in the file

---

## 📸 Screenshots

![Step 30](s3-versioning-img/30.png)  
![Step 31](s3-versioning-img/31.png)  
![Step 32](s3-versioning-img/32.png)  
![Step 33](s3-versioning-img/33.png)  
![Step 34](s3-versioning-img/34.png)

## 🔹 Step 7: Delete Specific Version & Keep Required Versions

In this step, I explored S3 Version control by managing multiple versions of the same file.

After uploading multiple versions, I found **4 different versions** with their respective **Version IDs**.

Since Version 2 and Version 3 were similar, I decided to remove the unnecessary version (Version 3).

### 🗑️ Delete Process:
- Went to the S3 bucket
- Enabled **Show versions**
- Selected the unwanted version (Version 3)
- Clicked on **Delete**
- Confirmed **Permanent Delete (Object Delete)**

---

### ✅ Result After Deletion:
- Version 3 was permanently deleted
- Now only **3 versions** remain in the bucket

---

## 📸 Screenshots

![Step 35](s3-versioning-img/35.png)  
![Step 36](s3-versioning-img/36.png)  
![Step 37](s3-versioning-img/37.png)

---

### 🎯 Key Learning:
- We can selectively delete specific versions in S3
- Unnecessary versions can be permanently removed
- Important versions can still be kept and accessed anytime
- This helps in better storage management and cost control

👉 This is how AWS S3 Versioning helps us manage file history efficiently.
