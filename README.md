# Preact

Preact là một thư viện JavaScript cho xây dựng giao diện người dùng dựa trên cú pháp và API của React, nhưng với kích thước nhỏ gọn và hiệu suất cao hơn.

### Ưu điểm

- **Kích thước nhẹ:** Preact có kích thước nhỏ hơn so với React. Điều này giúp giảm thời gian tải và tăng trải nghiệm người dùng, đặc biệt là trong các ứng dụng web di động.

- **Hiệu suất cao:** Thiết kế tối ưu của Preact giúp giữ được hiệu suất cao, đặc biệt là trong các ứng dụng có độ phức tạp cao.

- **Về độ tương thích React:** Preact sử dụng cú pháp và API tương tự như React, giúp cho việc chuyển đổi giữa hai thư viện dễ dàng. Điều này cho phép sử dụng cả hai trong một dự án mà không cần thay đổi lớn.

- **Hỗ trợ JSX:** Preact hỗ trợ JSX, giúp việc viết mã nguồn trở nên linh hoạt và dễ đọc.

> Mặc dù không lớn bằng cộng đồng của React, nhưng cộng đồng Preact vẫn tích cực và cung cấp hỗ trợ cho người dùng.

### Về nhược điểm

- **Dự án nhỏ hơn:** So với React, Preact có một cộng đồng và sinh động nhỏ hơn. Điều này có thể là một vấn đề nếu bạn đang tìm kiếm nhiều tài nguyên và plugins.

- **Không đầy đủ tính năng của React:** Preact không hỗ trợ một số tính năng của React như Context API hoặc một số lifecycle methods. Đối với một số dự án, điều này có thể tạo ra một số hạn chế.

- **Plugin và Thư viện ít hơn:** Số lượng plugin và thư viện cho Preact có thể ít hơn so với React, điều này có thể gây khó khăn cho các dự án đòi hỏi nhiều tính năng và mô-đun bổ sung.

### Cài đặt

- **Bạn có thể cài đặt Preact bằng npm:**

```JS
npm install preact
or
yarn add preact
```

### Một vài ví dụ dưới đây sẽ cho thấy sự khác biệt giữa preact và react

# **State, useState**

## Preact

```JSX
import { h, render, useState } from "preact";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```


## React

```JSX
import React, { useState } from 'react';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

> Cả hai đều sử dụng useState với cú pháp tương tự, mã nguồn giữa React và Preact có thể hoán đổi được mà không cần sửa đổi nhiều.

# **useEffect**

## Preact

```JSX
import { h, render, useState, useEffect } from 'preact';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

## React

```JSX
import React, { useEffect, useState } from 'react';

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

> Cả hai đều sử dụng useEffect để thực hiện các hành động sau khi component được render, cú pháp cũng tương tự nhau

# **Props**

## Preact

```JSX
import { h, render } from 'preact';

function ChildComponent(props) {
  return (
    <div>
      <p>Props Value: {props.value}</p>
      <button onClick={() => props.onChange('New Value')}>Change Value</button>
    </div>
  );
}

function ParentComponent() {
  const handleChange = (newValue) => {
    console.log(`Value changed to ${newValue}`);
  };

  return (
    <ChildComponent value="Default Value" onChange={handleChange} />
  );
}

render(<ParentComponent />, document.getElementById('app'));

```

## React

```JSX
import React from 'react';

function ChildComponent(props) {
  return (
    <div>
      <p>Props Value: {props.value}</p>
      <button onClick={() => props.onChange('New Value')}>Change Value</button>
    </div>
  );
}

function ParentComponent() {
  const handleChange = (newValue) => {
    console.log(`Value changed to ${newValue}`);
  };

  return (
    <ChildComponent value="Default Value" onChange={handleChange} />
  );
}

function App() {
  return (
    <ParentComponent />
  );
}

```

> Cú pháp sử dụng props giữa React và Preact là hoàn toàn tương tự, cả hai đều sử dụng props để truyền dữ liệu từ component cha đến component con, hành vi của props trong React và Preact là như nhau.

# **Context API**

## Preact

```JSX
import { h, render, createContext, useContext, useState } from 'preact';

const MyContext = createContext();

function ParentComponent({ children }) {
  const [value, setValue] = useState('Default Value');

  return (
    <MyContext.Provider value={{ value, setValue }}>
      {children}
    </MyContext.Provider>
  );
}

function ChildComponent() {
  const { value, setValue } = useContext(MyContext);

  return (
    <div>
      <p>Context Value: {value}</p>
      <button onClick={() => setValue('New Value')}>Change Value</button>
    </div>
  );
}

render(<ParentComponent><ChildComponent /></ParentComponent>, document.getElementById('app'));

```

## React

```JSX
import React, { createContext, useContext, useState } from 'react';

const MyContext = createContext();

function ParentComponent({ children }) {
  const [value, setValue] = useState('Default Value');

  return (
    <MyContext.Provider value={{ value, setValue }}>
      {children}
    </MyContext.Provider>
  );
}

function ChildComponent() {
  const { value, setValue } = useContext(MyContext);

  return (
    <div>
      <p>Context Value: {value}</p>
      <button onClick={() => setValue('New Value')}>Change Value</button>
    </div>
  );
}

function App() {
  return (
    <ParentComponent>
      <ChildComponent />
    </ParentComponent>
  );
}

```

> Cú pháp sử dụng Context API giữa React và Preact tương tự nhau, cả hai đều hỗ trợ việc chia sẻ dữ liệu giữa các component mà không cần truyền props qua nhiều cấp độ.

### Tổng kết

Nhìn chung, cả React và Preact sử dụng cú pháp và API tương đồng đối với các phương thức quan trọng như **state, useState, useEffect, context, và props.** Điều này giúp cho việc chuyển đổi giữa hai thư viện một cách dễ dàng và giữ cho mã nguồn linh hoạt và tái sử dụng được.

### Tài liệu tham khảo

[HERE](https://preactjs.com/)
