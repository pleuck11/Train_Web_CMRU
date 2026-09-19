# 🎓 Train Web CMRU — กิจกรรมพี่สอนน้อง

> โปรเจคฝึกปฏิบัติจากการอบรม **"พัฒนาเว็บแอปพลิเคชันด้วย Laravel & Livewire"**  
> จัดโดยกิจกรรมพี่สอนน้อง มหาวิทยาลัยราชภัฏเชียงใหม่ (CMRU)

---

## 📖 เกี่ยวกับโปรเจค

โปรเจคนี้เป็นผลงานที่ได้รับจากการเข้าร่วมกิจกรรม **พี่สอนน้อง** ของมหาวิทยาลัยราชภัฏเชียงใหม่  
โดยมุ่งเน้นการฝึกทักษะการพัฒนาเว็บแอปพลิเคชันด้วย **Laravel 12** และ **Livewire 4**  
ภายใต้สภาพแวดล้อม Docker ที่พร้อมใช้งานสำหรับนักศึกษาแต่ละคน

---

## 🛠️ Tech Stack

| เทคโนโลยี | เวอร์ชัน | หมายเหตุ |
|---|---|---|
| PHP | ^8.2 | Backend language |
| Laravel | ^12.0 | PHP Framework |
| Livewire | ^4.0 | Full-stack reactive components |
| Flux UI | ^2.9 | UI Component Library |
| Tailwind CSS | ^4.0 | Utility-first CSS |
| PostgreSQL | 16 | Relational Database |
| Nginx | alpine | Web Server |
| Docker | — | Containerization |
| Vite | ^7.0 | Frontend bundler |

---

## 📂 โครงสร้างโปรเจค

```
Train_Web_CMRU/
└── test-std{รหัสนักศึกษา}/   ← โฟลเดอร์ของนักศึกษาแต่ละคน
    ├── app/
    │   ├── Http/              ← Controllers & Middleware
    │   ├── Livewire/          ← Livewire Components
    │   ├── Models/            ← Eloquent Models
    │   └── Providers/
    ├── database/
    │   ├── migrations/        ← Database Migrations
    │   ├── factories/
    │   └── seeders/
    ├── resources/
    │   └── views/             ← Blade Templates
    ├── routes/                ← Route definitions
    ├── docker/                ← Nginx & Docker configs
    ├── docker-compose.yml
    ├── Dockerfile
    └── .env.example
```

---

## ⚙️ การตั้งค่าสภาพแวดล้อม (Setup)

### 1. Clone โปรเจค

```bash
git clone https://github.com/pleuck11/Train_Web_CMRU.git
cd Train_Web_CMRU/test-std{รหัสนักศึกษา}
```

### 2. ตั้งค่าไฟล์ `.env`

```bash
cp .env.example .env
```

แก้ไขค่าในไฟล์ `.env` ให้ตรงกับข้อมูลของตนเอง:

```dotenv
STUDENT_ID=std66xxxxxx        # รหัสนักศึกษา
STUDENT_NAME=std66xxxxxx      # ชื่อผู้ใช้ Docker
COMPOSE_PROJECT_NAME=std66xxxxxx
STUDENT_PORT=8000             # Port ที่ใช้เปิดเว็บ (ไม่ซ้ำกัน)
FORWARD_DB_PORT=5400          # Port สำหรับ PostgreSQL

DB_HOST=std66xxxxxx-db
DB_DATABASE=db_name
DB_USERNAME=db_66xxxxxx
DB_PASSWORD=db_password
```

### 3. รันด้วย Docker

```bash
# Build และ Start ทุก Services
docker compose up -d --build

# รัน Migrations และ Seeders
docker compose exec app php artisan migrate --seed

# Generate App Key (ถ้ายังไม่มี)
docker compose exec app php artisan key:generate
```

### 4. Build Frontend Assets

```bash
docker compose exec app npm run build
```

เปิดเบราว์เซอร์ที่ `http://localhost:{STUDENT_PORT}`

---

## 🚀 การพัฒนา (Development)

### รันแบบ Local (ไม่ใช้ Docker)

```bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
npm install

# รันทุกอย่างพร้อมกัน (PHP + Queue + Vite + Logs)
composer run dev
```

### คำสั่งที่ใช้บ่อย

```bash
# สร้าง Livewire Component
php artisan make:livewire ComponentName

# สร้าง Model + Migration
php artisan make:model ModelName -m

# ดู Routes ทั้งหมด
php artisan route:list

# รีเซ็ต Database
php artisan migrate:fresh --seed

# ตรวจสอบ Code Style
composer run lint

# รัน Tests
composer run test
```

---

## 🐳 Docker Services

| Service | Container | Port |
|---|---|---|
| Laravel App | `std{ID}-app` | — |
| Nginx | `std{ID}-nginx` | `{STUDENT_PORT}:80` |
| PostgreSQL | `std{ID}-db` | `{FORWARD_DB_PORT}:5432` |

```bash
# ดูสถานะ Containers
docker compose ps

# ดู Logs
docker compose logs -f

# หยุดทุก Services
docker compose down

# หยุดและลบ Volumes (ระวัง! ข้อมูลจะหาย)
docker compose down -v
```

---

## 🧪 การทดสอบ (Testing)

โปรเจคนี้ใช้ **Pest PHP** สำหรับการทดสอบ

```bash
# รัน Tests ทั้งหมด
php artisan test

# หรือผ่าน Composer
composer run test

# รัน Tests พร้อม Coverage
php artisan test --coverage
```

---

## 📋 ข้อมูลการอบรม

| รายการ | รายละเอียด |
|---|---|
| 🏫 สถาบัน | มหาวิทยาลัยราชภัฏเชียงใหม่ (CMRU) |
| 📅 กิจกรรม | พี่สอนน้อง |
| 🎯 วัตถุประสงค์ | ฝึกทักษะการพัฒนาเว็บด้วย Laravel & Livewire |
| 👨‍💻 กลุ่มเป้าหมาย | นักศึกษาสาขาคอมพิวเตอร์ |

---

## 📝 นักศึกษาที่เข้าร่วม

แต่ละโฟลเดอร์ `test-std{รหัสนักศึกษา}` คือโปรเจคของนักศึกษาแต่ละคน:

```
Train_Web_CMRU/
├── test-std66143432/   ← ตัวอย่าง (รหัส: 66143432)
└── test-std66xxxxxx/   ← นักศึกษาคนอื่นๆ
```

---

## 🤝 การมีส่วนร่วม

1. Fork โปรเจคนี้
2. สร้าง Branch ใหม่ (`git checkout -b feature/your-feature`)
3. Commit การเปลี่ยนแปลง (`git commit -m 'Add some feature'`)
4. Push ไปยัง Branch (`git push origin feature/your-feature`)
5. เปิด Pull Request

---

<div align="center">

Made with ❤️ at **CMRU — กิจกรรมพี่สอนน้อง**

🏫 มหาวิทยาลัยราชภัฏเชียงใหม่

</div>
