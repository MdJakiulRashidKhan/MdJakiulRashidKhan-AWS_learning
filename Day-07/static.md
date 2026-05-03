## 🪣 Step 1: Create S3 Bucket

First, I logged into the AWS Management Console and navigated to the S3 dashboard.

Then I created a new S3 bucket with the name:

`jakiul-static-website`

### Configuration:
- Unchecked **"Block all public access"** to allow public access
- Kept all other settings as default

Finally, the bucket was created successfully.

---

## 📷 Screenshots

![Step 1](static-img/1.png)
![Step 2](static-img/2.png)
![Step 3](static-img/3.png)
![Step 4](static-img/4.png)

## 📤 Step 2: Upload File & Enable Static Website Hosting

I went to the `jakiul-static-hosting` bucket and clicked on **Upload**.

Then I uploaded my file:
`portfolio.html`

After the upload was completed successfully, I closed the upload panel.

---

Next, I navigated to the **Properties** tab.

- Found **Static Website Hosting**
- Clicked **Edit**
- Enabled static website hosting
- Set the index document as:
  `portfolio.html`

Then I clicked **Save changes**.

---

After that, S3 generated a **website endpoint URL**.

When I opened the URL in the browser, it showed:
❌ **403 Forbidden**

This happened because the bucket policy was not configured yet.

---

## 🔐 Step 3: Add Bucket Policy

To fix the issue:

- I went to the **Permissions** tab  
- Clicked on **Edit** under Bucket Policy  

Since I didn’t have a predefined policy, I searched on Google and added a public read policy.

After adding the policy, I clicked **Save changes**.

---

## ✅ Result

Now when I opened the S3 website endpoint URL,  
the static website loaded successfully 🎉

---

## 📷 Screenshots

![Step 5](static-img/5.png)
![Step 6](static-img/6.png)
![Step 7](static-img/7.png)
![Step 8](static-img/8.png)
![Step 9](static-img/9.png)
![Step 10](static-img/10.png)
![Step 11](static-img/11.png)
![Step 12](static-img/12.png)
![Step 13](static-img/13.png)
![Step 14](static-img/14.png)
![Step 15](static-img/15.png)
![Step 16](static-img/16.png)
![Step 17](static-img/17.png)

## 📄 Step 4: Adding Custom 404 Error Page (Optional)

After successfully hosting the website, I added a custom error page to improve user experience.

---

### 📤 Upload 404 Page

I went to the S3 bucket:
`jakiul-static-hosting`

Then I clicked on **Upload** and added the file:

`404.html`

After the upload completed successfully, I closed the upload panel.

---

### ⚙️ Configure Error Document

Next, I navigated to:

**Properties → Static Website Hosting → Edit**

Then I configured:

- Error document: `404.html`

Finally, I saved the changes.

---

### 🌐 Result

Now, when a user tries to access a non-existing page,  
the custom **404.html error page** is displayed in the browser.

---

## 📷 Screenshots

![Step 18](static-img/18.png)
![Step 19](static-img/19.png)
![Step 20](static-img/20.png)
![Step 21](static-img/21.png)
![Step 25](static-img/25.png)
![Step 22](static-img/22.png)
