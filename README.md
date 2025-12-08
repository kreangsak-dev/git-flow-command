## First push main
```
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:kreangsak-dev/git-flow-command.git
git push -u origin main
```

## สร้างและสลับไป branch develop
```
git checkout -b develop
```

## Push develop ไปที่ server เพื่อเริ่ม tracking
```
git push -u origin develop
```

## สร้าง branch ชื่อ feature/multi-language
```
git checkout -b feature/multi-language
```

## รวมโค้ดกลับ (Merge & Pull Request)
```
git checkout develop
git pull origin develop  # ดึงโค้ดล่าสุดเผื่อมีใครแก้อะไร (ถ้าทำคนเดียวข้ามได้)
git merge feature/multi-language
```

# เตรียมขึ้น Production (Merge to Main)
```
git checkout main
git merge develop
git push origin main
```

## อัปเดตเลขเวอร์ชันในโค้ด (ทำที่ Develop)
```
ก่อนจะเอาขึ้น Main เราต้องแก้เลขเวอร์ชันในไฟล์โปรเจกต์ก่อน เพื่อให้โค้ดข้างในตรงกับ Tag ข้างนอก
อยู่ที่ branch develop
เปิดไฟล์ package.json
แก้บรรทัด "version": "0.1.0" ให้เป็น "1.0.0"
Commit การเปลี่ยนแปลงนี้
```
```
git add package.json
git commit -m "Bump version to 1.0.0"
```

## รวมโค้ดเข้า Main
```
git checkout main
git merge develop
git push origin main
```

## สร้าง Tag (ทำ Versioning)
### สร้าง Tag ชื่อ v1.0.0 พร้อมใส่คำอธิบาย
```
git tag -a v1.0.0 -m "Release version 1.0.0: Initial release with Multi-language support"
```

### Push Tag ขึ้น Server (Git ปกติจะไม่ push tag ให้ ต้องสั่งเอง)
```
git push origin --tags
```

## หลักการตั้งเลข Version (Semantic Versioning)
```
เพื่อให้ดูเป็นมาตรฐานสากล เรานิยมใช้ระบบ Major.Minor.Patch (เช่น 1.0.0)
หลักแรก (Major): เปลี่ยนเมื่อมีการเปลี่ยนแปลงใหญ่ ที่ของเก่าใช้ไม่ได้ (Breaking Change) หรือเปลี่ยนดีไซน์ใหม่หมด
ตัวอย่าง: 1.0.0 -> 2.0.0
หลักสอง (Minor): เปลี่ยนเมื่อมี Feature ใหม่ เพิ่มเข้ามา แต่ของเดิมยังทำงานได้ปกติ
ตัวอย่าง: เพิ่มระบบเปลี่ยนภาษาเสร็จ -> 1.0.0 -> 1.1.0
หลักสาม (Patch): เปลี่ยนเมื่อ แก้บั๊ก เล็กๆ น้อยๆ
ตัวอย่าง: แก้คำผิด, แก้ปุ่มกดไม่ได้ -> 1.0.1 -> 1.0.2
สรุปภาพรวม
Develop: แก้ไฟล์ package.json เปลี่ยนเลขเวอร์ชัน
Main: Merge เข้ามา
Main: สั่ง git tag แล้ว Push
```
