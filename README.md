# Tối ưu SEO với Next.js và Backend Node.js

Dự án này minh họa cách tối ưu SEO khi sử dụng Next.js kết hợp với backend Node.js, so sánh với phương pháp gọi API thông thường.

## Cấu trúc dự án

```
project/
├── frontend/           # Next.js frontend
│   ├── pages/
│   │   ├── index.js
│   │   └── api/
│   │       └── proxy.js
│   └── package.json
├── backend/            # Node.js backend
│   ├── server.js
│   └── package.json
└── README.md
```

## Backend (Node.js)

File: `backend/server.js`

```javascript
const express = require("express");
const app = express();
const port = 3001;
app.get("/api/products", (req, res) => {
  // Giả lập dữ liệu từ database
  const products = [
    { id: 1, name: "Product 1", description: "Description 1" },
    { id: 2, name: "Product 2", description: "Description 2" },
  ];
  res.json(products);
});
app.listen(port, () => {
  console.log(`Backend running on http://localhost:${port}`);
});
```

## Frontend (Next.js)

### 1. Phương pháp tối ưu SEO

File: `frontend/pages/index.js`

```javascript
import { useState, useEffect } from "react";
export async function getServerSideProps() {
  // Fetch dữ liệu từ backend tại server-side
  const res = await fetch("http://localhost:3001/api/products");
  const products = await res.json();
  return { props: { products } };
}
export default function Home({ products }) {
  return (
    <div>
      <h1>Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.name} - {product.description}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### 2. Phương pháp gọi API thông thường (không tối ưu SEO)

```javascript
import { useState, useEffect } from "react";
export default function Home() {
  const [products, setProducts] = useState([]);
  useEffect(() => {
    fetch("http://localhost:3001/api/products")
      .then((res) => res.json())
      .then((data) => setProducts(data));
  }, []);
  return (
    <div>
      <h1>Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.name} - {product.description}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

## So sánh hai phương pháp

1. Phương pháp tối ưu SEO (sử dụng `getServerSideProps`):

   - Dữ liệu được fetch tại server-side.
   - HTML đầy đủ được gửi đến client, bao gồm cả nội dung sản phẩm.
   - Tốt cho SEO vì search engines có thể đọc được nội dung ngay lập tức.
   - Trang load nhanh hơn đối với người dùng.

2. Phương pháp gọi API thông thường:
   - Dữ liệu được fetch tại client-side sau khi trang đã load.
   - Ban đầu, HTML không chứa dữ liệu sản phẩm.
   - Kém hiệu quả cho SEO vì search engines có thể không đợi để JavaScript fetch dữ liệu.
   - Có thể gây ra hiệu ứng nhấp nháy khi dữ liệu được load.

## Proxy API (Tùy chọn)

Để tránh vấn đề CORS, bạn có thể sử dụng API Routes của Next.js làm proxy:

File: `frontend/pages/api/proxy.js`

```javascript
export default function handler(req, res) {
  res.setHeader("Access-Control-Allow-Origin", "http://localhost:3000");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type");
  res.setHeader("Access-Control-Allow-Credentials", "true");
  res.json({ message: "Hello from Next.js!" });
}
```

Sau đó, trong `getServerSideProps`, bạn có thể gọi API này thay vì gọi trực tiếp đến backend:

```javascript
const res = await fetch("http://localhost:3000/api/proxy");
```

## Kết luận

Bằng cách sử dụng `getServerSideProps` của Next.js, chúng ta có thể tối ưu SEO khi làm việc với backend riêng biệt. Phương pháp này đảm bảo rằng nội dung được render ở server-side, cung cấp HTML đầy đủ cho search engines và cải thiện trải nghiệm người dùng.
