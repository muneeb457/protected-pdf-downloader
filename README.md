# 🚀 Google Drive Protected PDF Downloader

This project provides an efficient and secure method to download view-only protected PDF files from Google Drive using a browser script. By leveraging the powerful `jsPDF` library, this script seamlessly converts images into a downloadable PDF format.

---

## ✨ Features

✅ Download view-only protected PDFs directly from Google Drive.  
✅ Convert images from the page into a single high-quality PDF file.  
✅ Secure script execution using the Trusted Types API.  
✅ No additional software or extensions required—works directly in your browser.  

---

## 📌 Requirements

- A modern web browser supporting the Trusted Types API and JavaScript.
- Access to view the PDF files on Google Drive.

---

## 📖 How to Use

1️⃣ **Open the PDF in Google Drive**: Navigate to the view-only PDF you want to download.  
2️⃣ **Run the Script**:
   - Open your browser's **Developer Tools** (Press `F12` or right-click → Inspect).
   - Navigate to the **Console** tab.
   - Copy and paste the script below into the console and press **Enter**.

```javascript
const loadScript = (src, callback) => {
    let script = document.createElement('script');
    script.src = src;
    script.onload = callback;
    document.body.appendChild(script);
};

loadScript('https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js', () => {
    const { jsPDF } = window.jspdf;
    let pdf = new jsPDF();
    let images = document.querySelectorAll('img');
    let isFirstPage = true;

    images.forEach((img, index) => {
        if (!img.src.startsWith('blob:')) return;

        let canvas = document.createElement('canvas');
        let ctx = canvas.getContext('2d');
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0, img.width, img.height);
        let imgData = canvas.toDataURL('image/jpeg', 1.0);

        let imgWidth = 210; // A4 size width in mm
        let imgHeight = (canvas.height * imgWidth) / canvas.width;

        if (!isFirstPage) pdf.addPage();
        pdf.addImage(imgData, 'JPEG', 0, 0, imgWidth, imgHeight);
        isFirstPage = false;
    });

    pdf.save('download.pdf');
});
```

3️⃣ **Download the PDF**: The script will generate a PDF file containing the extracted images and prompt you to download it.  

---

## ⚠️ Disclaimer

⚠️ This script is intended **only for personal use** or with explicit permission from the content owner.  
⚠️ The authors **do not take any responsibility** for any misuse of this tool.  

---

## 🤝 Contributing

Have suggestions or improvements? Feel free to create a **pull request** or **open an issue** on GitHub. Contributions are always welcome! 🚀

---

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---
