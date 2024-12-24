<!DOCTYPE html>  
<html lang="ar">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>تحديث البيانات تلقائيًا</title>  
</head>  
<body>  
    <h1>أدخل البيانات الجديدة</h1>  
    <form id="dataForm">  
        <label for="fullName">الاسم الكامل:</label><br>  
        <input type="text" id="fullName" required><br><br>  

        <label for="deviceName">اسم الجهاز:</label><br>  
        <input type="text" id="deviceName" required><br><br>  

        <label for="age">العمر:</label><br>  
        <input type="number" id="age" required><br><br>  

        <label for="location">المكان:</label><br>  
        <input type="text" id="location" required><br><br>  

        <button type="submit">إرسال</button>  
    </form>  

    <script>  
        document.getElementById('dataForm').addEventListener('submit', async (e) => {  
            e.preventDefault(); // منع إعادة تحميل الصفحة  

            // اجمع البيانات من الحقول  
            const fullName = document.getElementById('fullName').value;  
            const deviceName = document.getElementById('deviceName').value;  
            const age = document.getElementById('age').value;  
            const location = document.getElementById('location').value;  

            // إعداد المتغيرات  
            const token = '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'; // استبدل برمز الوصول الخاص بك  
            const repo = 'yousefmrim
            /YOUR_REPO'; mariamyousef486   
            const filePath = 'YOUR_FILE_PATH'; // استبدل بمسار الملف الذي ترغب في تحديثه  

            // اجمع المعلومات في صيغة نصية  
            const newData = `الاسم الكامل: ${fullName}\nاسم الجهاز: ${deviceName}\nالعمر: ${age}\nالمكان: ${location}\n`;  

            // استخدم GitHub API للحصول على SHA للملف الحالي  
            const getFileResponse = await fetch(`https://api.github.com/repos/${repo}/contents/${filePath}`, {  
                headers: {  
                    'Authorization': `token ${token}`  
                }  
            });  

            if (!getFileResponse.ok) {  
                alert('فشل في الحصول على الملف. تحقق من إعدادات المستودع أو المسار.');  
                return;  
            }  
            
            const fileData = await getFileResponse.json();  
            const sha = fileData.sha;  

            // تحديث المحتوى  
            const updatedContent = btoa(newData); // تحويل النص إلى Base64  
            const updateResponse = await fetch(`https://api.github.com/repos/${repo}/contents/${filePath}`, {  
                method: 'PUT',  
                headers: {  
                    'Content-Type': 'application/json',  
                    'Authorization': `token ${token}`  
                },  
                body: JSON.stringify({  
                    message: 'تحديث البيانات تلقائيًا',  
                    content: updatedContent,  
                    sha: sha // استخدام SHA للملف الحالي  
                })  
            });  

            if (updateResponse.ok) {  
                alert('تم تحديث البيانات بنجاح!');  
            } else {  
                alert('فشل تحديث البيانات. تحقق من الأخطاء.');  
            }  
        });  
    </script>  
</body>  
</html>
