<h1 align="center">LIS System</h1>

This product is a laboratory information management system. The system comprehensively manages laboratory testing activities in medical facilities. The system provides features for managing test orders, test results, test equipment, connectivity, information exchange with HIS medical record management systems and some system administration features. The system can be developed into a standalone system in medical facility laboratories or integrated with existing medical record management and hospital management systems in those facilities.

# Table of Contents

- [Table of Contents](#table-of-contents)
- [General structure of the project](#general-structure-of-the-project)
  - [Frontend: React + TypeScript](#frontend-react--typescript)
  - [Backend: Node.js + TypeScript (Module hóa)](#backend-nodejs--typescript-module-hóa)
- [Luồng hoạt động của hệ thống](#luồng-hoạt-động-của-hệ-thống)
  - [Bảo mật và quản lý dữ liệu](#bảo-mật-và-quản-lý-dữ-liệu)

# General structure of the project

```
/LIS-Management-System
├── frontend/                    # Frontend (React + TypeScript)
├── backend/                     # Backend (Node.js + TypeScript)
├── docs/                        # Tài liệu dự án
├── .env                         # Biến môi trường chung
└── README.md                    # Thông tin dự án và hướng dẫn sử dụng
```

## Frontend: React + TypeScript

```
frontend/
├── public/                      # Chứa các tệp tĩnh
│   └── index.html               # Tệp HTML chính
├── src/
│   ├── assets/                  # Các tài nguyên như hình ảnh, fonts, icons
│   ├── components/              # Các component nhỏ, tái sử dụng như Button, Input
│   ├── containers/              # Chứa các component với logic phức tạp, có thể gọi API
│   ├── services/                # Xử lý gọi API từ backend
│   ├── hooks/                   # Chứa các custom hooks cho logic chung
│   ├── pages/                   # Các trang tương ứng với các route của ứng dụng
│   ├── routes/                  # Định nghĩa các tuyến đường của ứng dụng
│   ├── store/                   # Quản lý state toàn cục, sử dụng Redux hoặc Context API
│   ├── theme/                   # Định nghĩa styles, theme chung cho toàn ứng dụng
│   ├── types/                   # Định nghĩa các types và interface trong TypeScript
│   ├── utils/                   # Các hàm tiện ích dùng chung
│   └── index.tsx                # Điểm entry chính của ứng dụng React
├── tsconfig.json                # Cấu hình TypeScript
└── package.json                 # Thông tin và dependencies của frontend
```

- **Giải thích chi tiết:**
  - **public/**: Chứa các tài nguyên công khai như favicon, tệp HTML gốc để render React app.
  - **assets/**: Chứa hình ảnh, biểu tượng, fonts, phục vụ cho giao diện người dùng.
  - **components/**: Các thành phần UI nhỏ như nút bấm, biểu mẫu, chỉ nhận dữ liệu từ [props](https://viblo.asia/p/su-khac-nhau-giua-props-va-state-trong-reactjs-gGJ59GBPZX2).
  - **containers/**: Kết hợp các component để tạo ra các khối logic lớn hơn và kết nối với dữ liệu từ API.
  - **services/**: Chứa các hàm xử lý API, ví dụ gọi đến backend để lấy dữ liệu.
  - **hooks/**: Custom hooks để quản lý trạng thái và các logic dùng lại.
  - **pages/**: Chứa các trang cụ thể của ứng dụng, mỗi route sẽ tương ứng với một page.
  - **routes/**: Định nghĩa các đường dẫn của ứng dụng, kết nối với các page.
  - **store/**: Sử dụng Redux hoặc Context API để quản lý state toàn cục.
  - **theme/**: Định nghĩa chung về giao diện (theme), bao gồm màu sắc, kích thước font.
  - **types/**: Các kiểu dữ liệu trong TypeScript để đảm bảo tính an toàn của kiểu.
  - **utils/**: Các hàm tiện ích chung, ví dụ như định dạng dữ liệu, xử lý logic chung.

## Backend: Node.js + TypeScript (Module hóa)

```
backend/
├── src/
│   ├── modules/
│   │   ├── module_user/                # Module quản lý người dùng
│   │   │   ├── user.controller.ts
│   │   │   ├── user.service.ts
│   │   │   ├── user.model.ts
│   │   │   ├── user.route.ts
│   │   └── test/                # Module quản lý xét nghiệm
│   │       ├── test.controller.ts
│   │       ├── test.service.ts
│   │       ├── test.model.ts
│   │       ├── test.route.ts
│   ├── config/                  # Cấu hình cho hệ thống (DB, môi trường, JWT)
│   ├── middlewares/             # Các middleware chung như xác thực, logging
│   ├── utils/                   # Các hàm tiện ích, xử lý mã hóa, logging
│   ├── app.ts                   # Khởi tạo Express server và kết nối các module
│   └── server.ts                # Entry point khởi chạy server
├── .env                         # Biến môi trường (DB connection, JWT secret)
├── tsconfig.json                # Cấu hình TypeScript
└── package.json                 # Thông tin, dependencies của backend
```

- **Giải thích chi tiết:**
  - **modules/**: Mỗi module trong backend chịu trách nhiệm xử lý một phần nghiệp vụ của hệ thống, được chia thành các file controller, service, model, repository, và route:
  - **user/**: Module xử lý người dùng (đăng ký, đăng nhập, quản lý thông tin cá nhân).
  - **test/**: Module quản lý xét nghiệm (tạo, cập nhật, lấy kết quả xét nghiệm).
  - **config/**: Cấu hình môi trường, kết nối cơ sở dữ liệu, JWT secret, v.v.
  - **middlewares/**: Chứa các middleware chung cho ứng dụng như xác thực, logging.
  - **utils/**: Các hàm tiện ích dùng trong nhiều module như mã hóa dữ liệu, xử lý lỗi.
  - **app.ts**: Khởi tạo Express server và kết nối các route của module lại với nhau.
  - **server.ts**: Điểm entry chính của server, bắt đầu lắng nghe các request HTTP.

# Luồng hoạt động của hệ thống

1. **Frontend (React):** Khi người dùng truy cập vào ứng dụng, frontend sẽ render giao diện từ các component. Các action như đăng nhập, lấy danh sách xét nghiệm sẽ gửi request API đến backend.

2. **Backend (Node.js):**

- Routes trong backend sẽ nhận request từ frontend và gọi đến các controllers để xử lý.
- Controllers nhận yêu cầu, chuyển tiếp đến các services để xử lý logic nghiệp vụ. Nếu có liên quan đến cơ sở dữ liệu, các services sẽ gọi đến repositories để lấy hoặc ghi dữ liệu.
- Dữ liệu được trả về frontend dưới dạng JSON để hiển thị cho người dùng.

3. Frontend nhận dữ liệu, cập nhật vào store (Redux/Context API) và render lại giao diện phù hợp.

## Bảo mật và quản lý dữ liệu

- JWT: Dùng để xác thực người dùng, bảo mật các API.
- Bcrypt: Mã hóa mật khẩu trước khi lưu trữ.
- Rate limiting và CORS: Bảo vệ API khỏi tấn công brute-force và điều chỉnh quyền truy cập.
- HTTPS: Sử dụng để mã hóa dữ liệu trao đổi giữa client và server.
