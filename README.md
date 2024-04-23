# บันทึกประจำวัน - 23 เมษายน พ.ศ. 2567

## รายละเอียด API

### เทคโนโลยีที่ใช้:
- Fiber (เฟรมเวิร์คสำหรับ Go)
- Gorm (ORM สำหรับ Go)

### Endpoints:

#### 1. Login
- **วิธีการ:** POST
- **เอ็นด์พอยท์:** `localhost:8080/api/v1/auth/login`
- **ข้อมูลร้องขอ (Request Body):**
  {
    "username": "example",
    "password": "example"
  }
- **การตอบกลับ (Response):**
  {
    "jwt": "<JWT_TOKEN>",
  }
- **ด้านใน JWT***
    {
        "uuid": "<USER_UUID>",
        "exp": "<EXPIRATION_TIME>"
        "iat": "<ISSUED_AT>"
    }

#### 2. Register
- **วิธีการ:** POST
- **เอ็นด์พอยท์:** `localhost:8080/api/v1/auth/register`
- **ข้อมูลร้องขอ (Request Body):**
  {
    "username": "example",
    "password": "example",
    "email": "example@example.com"
  }
- **การตอบกลับ (Response):**
  {
    "uuid": "<USER_UUID>"
  }

#### 3. Upload Image
- **วิธีการ:** PUT with Authorization Header
- **เอ็นด์พอยท์:** `localhost:8080/api/v1/authorized/user/avatar/me`
- **ข้อมูลร้องขอ (Request Body):** (multipart/form-data)
  {
    "image": <IMAGE_FILE>
  }
- **การตอบกลับ (Response):** (สถานะโค้ด: 200 OK)

#### 4. Get Image
- **วิธีการ:** GET with Authorization Header
- **เอ็นด์พอยท์:** `localhost:8080/api/v1/authorized/user/avatar/me`
- **การตอบกลับ (Response):** (ไฟล์รูปภาพ)

## แบบแอปพลิเคชัน Svelte

### เทคโนโลยีที่ใช้:
- Svelte (เฟรมเวิร์คสำหรับ JavaScript)
- Tailwind CSS (เฟรมเวิร์ค CSS แบบ Utility-First)

### หน้า:

#### 1. หน้าเข้าสู่ระบบ (Login Page)
- ช่องทางสำหรับผู้ใช้เข้าสู่ระบบ
- เก็บโทเค็น JWT ใน localStorage เมื่อเข้าสู่ระบบสำเร็จ

#### 2. หน้าลงทะเบียน (Register Page)
- ช่องทางสำหรับผู้ใช้ลงทะเบียน

#### 3. หน้าอัปโหลดรูปภาพ (Upload Image Page)
- ช่องทางสำหรับผู้ใช้อัปโหลดรูปภาพ

### อ้างอิง:
- Fiber Documentation: [https://docs.gofiber.io/](https://docs.gofiber.io/)
- Gorm Documentation: [https://gorm.io/](https://gorm.io/)
- Tailwind Components: [https://tailwindcomponents.com/](https://tailwindcomponents.com/)
