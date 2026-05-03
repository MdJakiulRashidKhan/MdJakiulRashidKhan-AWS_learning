# 🚀 AWS S3 Bucket Practice – Pre-Signed URL Demo

আজকে আমি AWS S3 নিয়ে একটি hands-on practice করেছি যেখানে bucket তৈরি, file upload এবং file access test করেছি।

---

## 🛠️ What I did:

আমি Amazon Web Services এর S3 service এ গিয়ে একটি bucket create করেছি।

- Bucket Name: `jakiul-pre-signed-url-demo`
- সব settings default রেখে bucket create করেছি

তারপর bucket এর ভিতরে গিয়ে:

- Add files থেকে `1.txt` file upload করেছি  
- Successfully upload হয়েছে  

Upload করা file এ গিয়ে:

- `1.txt` file open করেছি  
- Browser এ file content দেখতে পেরেছি  

---

## 📸 Screenshot

![img](presigned-img1)
![img](presigned-img2)
![img](presigned-img3)
![img](presigned-img4)
![img](presigned-img5)
![img](presigned-img6)
![img](presigned-img7)
![img](presigned-img8)

---

# 🔗 AWS S3 Pre-Signed URL Demo (Temporary Access)

আজকে আমি AWS S3 ব্যবহার করে একটি object এর জন্য **Pre-Signed URL generate করে temporary access share করার practice করেছি।

---

## 🛠️ What I did:

আমি :contentReference[oaicite:0]{index=0} এর **Amazon S3** service এ গিয়ে আমার uploaded object এর জন্য pre-signed URL তৈরি করেছি।

### 🔹 Steps:

- Object (1.txt) select করেছি  
- **Actions** এ গিয়ে **Share with a pre-signed URL** option এ গিয়েছি  
- Access time হিসেবে **1 minute** select করেছি  
- তারপর **Create pre-signed URL** এ click করেছি  
- Generated URL copy করেছি  

---

## 🌐 Testing the URL

- আমি copied pre-signed URL টা **incognito mode** এ paste করেছি  
- File এর content successfully browser এ দেখা গেছে ✔️  
- কিন্তু 1 minute পরে URL expire হয়ে গেছে এবং access error দেখাচ্ছে ❌  

---

## 📸 Screenshot

![img](presigned-img9)
![img](presigned-img10)
![img](presigned-img11)
![img](presigned-img12)
![img](presigned-img13)
![img](presigned-img14)

---

## 🎯 Conclusion

এই hands-on practice এর মাধ্যমে আমি AWS S3 এর একটি complete basic workflow ভালোভাবে বুঝতে পেরেছি।

আমি প্রথমে একটি S3 bucket তৈরি করেছি এবং সেখানে একটি simple text file (`1.txt`) upload করেছি। এরপর আমি দেখেছি কীভাবে AWS S3 object storage এ file রাখা এবং browser এর মাধ্যমে access করা যায়।

পরবর্তীতে আমি Pre-Signed URL ব্যবহার করে একটি temporary secure access link generate করেছি। সেখানে আমি access time হিসেবে 1 minute set করেছি, যাতে নির্দিষ্ট সময়ের জন্যই file টি দেখা যায়।

Incognito mode এ URL test করার পর দেখা গেছে যে file নির্দিষ্ট সময়ের মধ্যে access করা যাচ্ছে, কিন্তু 1 minute পরে URL automatically expire হয়ে গেছে এবং access বন্ধ হয়ে গেছে।

এই পুরো process থেকে আমি শিখেছি যে Pre-Signed URL ব্যবহার করে আমরা কোনো S3 object কে secure ভাবে limited time এর জন্য share করতে পারি, যা security এবং controlled access এর জন্য খুবই গুরুত্বপূর্ণ।

👉 সংক্ষেপে:
- S3 bucket তৈরি ও file upload  
- Object browser থেকে access করা  
- Pre-Signed URL generate করা  
- Time-based temporary secure access বোঝা  


