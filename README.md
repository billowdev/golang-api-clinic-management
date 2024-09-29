# api-clinic-management
Example api on go in clinic management usecaase and ER Diagram


# Business Context


## Employee Table

**Description**: แสดงรายละเอียดของพนักงานในระบบ

| Column Name     | Data Type     | Constraints                              | Description                                               |
|-----------------|---------------|------------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                   | รหัสประจำตัวพนักงานที่ไม่ซ้ำกัน.                        |
| `name`          | `VARCHAR(100)` |                                          | ชื่อพนักงาน.                                           |
| `surname`       | `VARCHAR(100)` |                                          | นามสกุลพนักงาน.                                       |
| `email`         | `VARCHAR(255)` |                                          | อีเมลของพนักงาน.                                     |
| `username`      | `VARCHAR(100)` |                                          | ชื่อผู้ใช้สำหรับเข้าระบบ.                             |
| `password`      | `VARCHAR(255)` |                                          | รหัสผ่านของพนักงาน.                                   |
| `sex`           | `VARCHAR(10)`  |                                          | เพศของพนักงาน.                                       |
| `phone`         | `VARCHAR(20)`  |                                          | เบอร์โทรศัพท์ของพนักงาน.                             |
| `permission`    | `PermissionEnum`|                                       | สิทธิการเข้าถึงของพนักงาน (เจ้าของ, พนักงาน).        |
| `address`       | `VARCHAR(255)` |                                          | ที่อยู่เลขที่/หมู่.                                    |
| `subdistrict`   | `VARCHAR(100)` |                                          | ตำบลของพนักงาน.                                      |
| `district`      | `VARCHAR(100)` |                                          | อำเภอของพนักงาน.                                     |
| `province`      | `VARCHAR(100)` |                                          | จังหวัดของพนักงาน.                                   |
| `zipcode`       | `VARCHAR(10)`  |                                          | รหัสไปรษณีย์ของพนักงาน.                             |
| `created_at`    | `TIMESTAMP`    | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was created.                   |
| `updated_at`    | `TIMESTAMP`    | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำตัวพนักงานที่ไม่ซ้ำกัน.
- `permission` ใช้เพื่อกำหนดสิทธิการเข้าถึงของพนักงาน.

```sql
Table Employee [NOTE: "ข้อมูลพนักงาน แสดงรายละเอียดของพนักงานในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำตัวพนักงานที่ไม่ซ้ำกัน."]
  name VARCHAR(100) [NOTE: "ชื่อพนักงาน."]
  surname VARCHAR(100) [NOTE: "นามสกุลพนักงาน."]
  email VARCHAR(255) [NOTE: "อีเมลของพนักงาน."]
  username VARCHAR(100) [NOTE: "ชื่อผู้ใช้สำหรับเข้าระบบ."]
  password VARCHAR(255) [NOTE: "รหัสผ่านของพนักงาน."]
  sex VARCHAR(10) [NOTE: "เพศของพนักงาน."]
  phone VARCHAR(20) [NOTE: "เบอร์โทรศัพท์ของพนักงาน."]
  permission PermissionEnum [NOTE: "สิทธิการเข้าถึงของพนักงาน (เจ้าของ, พนักงาน)."]
  address VARCHAR(255) [NOTE: "ที่อยู่เลขที่/หมู่."]
  subdistrict VARCHAR(100) [NOTE: "ตำบลของพนักงาน."]
  district VARCHAR(100) [NOTE: "อำเภอของพนักงาน."]
  province VARCHAR(100) [NOTE: "จังหวัดของพนักงาน."]
  zipcode VARCHAR(10) [NOTE: "รหัสไปรษณีย์ของพนักงาน."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Doctor Table

**Description**: ตารางสำหรับข้อมูลแพทย์ แสดงรายละเอียดของแพทย์ในระบบ

| Column Name          | Data Type     | Constraints                        | Description                                   |
|-----------------------|---------------|------------------------------------|-----------------------------------------------|
| `id`                  | `UUID`        | `PRIMARY KEY`, `UNIQUE`           | รหัสประจำตัวแพทย์ที่ไม่ซ้ำกัน.                 |
| `employee_id`         | `UUID`        | `REFERENCES Employee(id)`          | อ้างอิงถึงข้อมูลพนักงาน (แพทย์).              |
| `specialization`      | `VARCHAR(100)`|                                    | ความเชี่ยวชาญของแพทย์.                      |
| `license_number`      | `VARCHAR(100)`|                                    | หมายเลขใบอนุญาตแพทย์.                       |
| `registration_date`   | `TIMESTAMP`   |                                    | วันที่ลงทะเบียนเป็นแพทย์.                    |
| `experience_years`    | `INT`         |                                    | จำนวนปีที่มีประสบการณ์.                      |
| `created_at`          | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`        | Timestamp when the record was created.       |
| `updated_at`          | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`        | Timestamp when the record was last updated.  |

**Notes**:
- `id`: รหัสประจำตัวแพทย์ที่ไม่ซ้ำกัน.
- `employee_id`: อ้างอิงถึงข้อมูลพนักงาน (แพทย์).
- `specialization`: ความเชี่ยวชาญของแพทย์.
- `license_number`: หมายเลขใบอนุญาตแพทย์.
- `registration_date`: วันที่ลงทะเบียนเป็นแพทย์.
- `experience_years`: จำนวนปีที่มีประสบการณ์.
- `created_at`: Timestamp when the record was created.
- `updated_at`: Timestamp when the record was last updated.

```sql
Table Doctor [NOTE: "ข้อมูลแพทย์ แสดงรายละเอียดของแพทย์ในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำตัวแพทย์ที่ไม่ซ้ำกัน."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงาน (แพทย์)."]
  specialization VARCHAR(100) [NOTE: "ความเชี่ยวชาญของแพทย์."]
  license_number VARCHAR(100) [NOTE: "หมายเลขใบอนุญาตแพทย์."]
  registration_date TIMESTAMP [NOTE: "วันที่ลงทะเบียนเป็นแพทย์."]
  experience_years INT [NOTE: "จำนวนปีที่มีประสบการณ์."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Patient Management

**Description**: แสดงรายละเอียดของคนไข้ในระบบ

| Column Name     | Data Type     | Constraints                              | Description                                               |
|-----------------|---------------|------------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                   | รหัสประจำคนไข้ที่ไม่ซ้ำกัน.                             |
| `name`          | `VARCHAR(100)` |                                          | ชื่อคนไข้.                                             |
| `surname`       | `VARCHAR(100)` |                                          | นามสกุลคนไข้.                                         |
| `id_card`       | `VARCHAR(20)`  |                                          | รหัสประจำตัวประชาชนของคนไข้.                          |
| `sex`           | `VARCHAR(10)`  |                                          | เพศของคนไข้.                                         |
| `birth_date`    | `DATE`        |                                          | วันเกิดของคนไข้.                                       |
| `blood_type`    | `VARCHAR(10)`  |                                          | กรุ๊ปเลือดของคนไข้.                                   |
| `disease`       | `TEXT`        |                                          | โรคประจำตัวของคนไข้.                                   |
| `allergic`      | `TEXT`        |                                          | ประวัติการแพ้ของคนไข้.                                 |
| `phone`         | `VARCHAR(20)`  |                                          | เบอร์โทรศัพท์ของคนไข้.                                 |
| `address`       | `VARCHAR(255)` |                                          | ที่อยู่เลขที่/หมู่.                                      |
| `subdistrict`   | `VARCHAR(100)` |                                          | ตำบลของคนไข้.                                        |
| `district`      | `VARCHAR(100)` |                                          | อำเภอของคนไข้.                                       |
| `province`      | `VARCHAR(100)` |                                          | จังหวัดของคนไข้.                                     |
| `zipcode`       | `VARCHAR(10)`  |                                          | รหัสไปรษณีย์ของคนไข้.                                 |
| `created_at`    | `TIMESTAMP`    | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was created.                   |
| `updated_at`    | `TIMESTAMP`    | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำคนไข้ที่ไม่ซ้ำกัน.

```sql
Table Patient [NOTE: "ข้อมูลคนไข้ แสดงรายละเอียดของคนไข้ในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำคนไข้ที่ไม่ซ้ำกัน."]
  name VARCHAR(100) [NOTE: "ชื่อคนไข้."]
  surname VARCHAR(100) [NOTE: "นามสกุลคนไข้."]
  id_card VARCHAR(20) [NOTE: "รหัสประจำตัวประชาชนของคนไข้."]
  sex VARCHAR(10) [NOTE: "เพศของคนไข้."]
  birth_date DATE [NOTE: "วันเกิดของคนไข้."]
  blood_type VARCHAR(10) [NOTE: "กรุ๊ปเลือดของคนไข้."]
  disease TEXT [NOTE: "โรคประจำตัวของคนไข้."]
  allergic TEXT [NOTE: "ประวัติการแพ้ของคนไข้."]
  phone VARCHAR(20) [NOTE: "เบอร์โทรศัพท์ของคนไข้."]
  address VARCHAR(255) [NOTE: "ที่อยู่เลขที่/หมู่."]
  subdistrict VARCHAR(100) [NOTE: "ตำบลของคนไข้."]
  district VARCHAR(100) [NOTE: "อำเภอของคนไข้."]
  province VARCHAR(100) [NOTE: "จังหวัดของคนไข้."]
  zipcode VARCHAR(10) [NOTE: "รหัสไปรษณีย์ของคนไข้."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Appointment Management

**Description**: แสดงรายละเอียดการนัดหมายระหว่างพนักงานกับคนไข้

| Column Name     | Data Type     | Constraints                              | Description                                               |
|-----------------|---------------|------------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                   | รหัสประจำตารางการนัดหมายที่ไม่ซ้ำกัน.                   |
| `subject`       | `VARCHAR(255)` |                                          | หัวข้อของการนัดหมาย.                                   |
| `detail`        | `TEXT`        |                                          | รายละเอียดของการนัดหมาย.                               |
| `date`          | `TIMESTAMP`   |                                          | วันที่นัดหมาย.                                         |
| `status`        | `VARCHAR(100)` |                                          | สถานะการนัดหมาย (เช่น 'Pending', 'Completed').        |
| `patient_id`    | `UUID`        | `REFERENCES Patient(id)`                | อ้างอิงถึงข้อมูลคนไข้ที่นัดหมาย.                      |
| `employee_id`   | `UUID`        | `REFERENCES Employee(id)`               | อ้างอิงถึงข้อมูลพนักงานที่จัดนัดหมาย.                  |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was created.                   |
| `updated_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`             | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำตารางการนัดหมายที่ไม่ซ้ำกัน.

```sql
Table Appointment [NOTE: "ข้อมูลการนัดหมาย แสดงรายละเอียดการนัดหมายระหว่างพนักงานกับคนไข้"] {
  id UUID [pk, unique, NOTE: "รหัสประจำตารางการนัดหมายที่ไม่ซ้ำกัน."]
  subject VARCHAR(255) [NOTE: "หัวข้อของการนัดหมาย."]
  detail TEXT [NOTE: "รายละเอียดของการนัดหมาย."]
  date TIMESTAMP [NOTE: "วันที่นัดหมาย."]
  status VARCHAR(100) [NOTE: "สถานะการนัดหมาย (เช่น 'Pending', 'Completed')."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้ที่นัดหมาย."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงานที่จัดนัดหมาย."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Material Management

**Description**: แสดงรายละเอียดวัสดุในระบบ

| Column Name      | Data Type     | Constraints                             | Description                                               |
|------------------|---------------|-----------------------------------------|-----------------------------------------------------------|
| `id`             | `UUID`        | `PRIMARY KEY, UNIQUE`                  | รหัสประจำวัสดุที่ไม่ซ้ำกัน.                               |
| `name`           | `VARCHAR(255)` |                                         | ชื่อวัสดุ.                                             |
| `detail`         | `TEXT`        |                                         | รายละเอียดวัสดุ.                                       |
| `unit`           | `VARCHAR(50)`  |                                         | หน่วยนับของวัสดุ.                                     |
| `purchase_price` | `DECIMAL(10, 2)` |                                     | ราคาซื้อวัสดุ.                                       |
| `qty`            | `INT`         |                                         | จำนวนวัสดุในสต็อก.                                   |
| `agent_id`       | `UUID`        | `REFERENCES Agent(id)`                 | อ้างอิงถึงข้อมูลตัวแทนจำหน่าย.                          |
| `created_at`     | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was created.                   |
| `updated_at`     | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำวัสดุที่ไม่ซ้ำกัน.

```sql
Table Material [NOTE: "ข้อมูลวัสดุ แสดงรายละเอียดของวัสดุในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำวัสดุที่ไม่ซ้ำกัน."]
  name VARCHAR(255) [NOTE: "ชื่อวัสดุ."]
  detail TEXT [NOTE: "รายละเอียดวัสดุ."]
  unit VARCHAR(50) [NOTE: "หน่วยนับของวัสดุ."]
  purchase_price DECIMAL(10, 2) [NOTE: "ราคาซื้อวัสดุ."]
  qty INT [NOTE: "จำนวนวัสดุในสต็อก."]
  agent_id UUID [ref: > Agent.id, NOTE: "อ้างอิงถึงข้อมูลตัวแทนจำหน่าย."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```


## Material Order Management

**Description**: แสดงรายละเอียดการสั่งซื้อวัสดุ

| Column Name      | Data Type     | Constraints                             | Description                                               |
|------------------|---------------|-----------------------------------------|-----------------------------------------------------------|
| `id`             | `UUID`        | `PRIMARY KEY, UNIQUE`                  | รหัสการสั่งซื้อวัสดุที่ไม่ซ้ำกัน.                        |
| `total_price`    | `DECIMAL(10, 2)` |                                     | ราคารวมของการสั่งซื้อ.                                   |
| `purchase_date`  | `DATE`        |                                         | วันที่ทำการสั่งซื้อ.                                     |
| `receive_date`   | `DATE`        |                                         | วันที่ได้รับวัสดุ.                                       |
| `status`         | `VARCHAR(100)` |                                        | สถานะการสั่งซื้อ.                                       |
| `employee_id`    | `UUID`        | `REFERENCES Employee(id)`               | อ้างอิงถึงข้อมูลพนักงานที่ทำการสั่งซื้อ.                 |
| `agent_id`       | `UUID`        | `REFERENCES Agent(id)`                 | อ้างอิงถึงข้อมูลตัวแทนจำหน่าย.                           |
| `created_at`     | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was created.                   |
| `updated_at`     | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสการสั่งซื้อวัสดุที่ไม่ซ้ำกัน.

```sql
Table MaterialOrder [NOTE: "ข้อมูลการสั่งซื้อวัสดุ แสดงรายละเอียดการสั่งซื้อวัสดุ"] {
  id UUID [pk, unique, NOTE: "รหัสการสั่งซื้อวัสดุที่ไม่ซ้ำกัน."]
  total_price DECIMAL(10, 2) [NOTE: "ราคารวมของการสั่งซื้อ."]
  purchase_date DATE [NOTE: "วันที่ทำการสั่งซื้อ."]
  receive_date DATE [NOTE: "วันที่ได้รับวัสดุ."]
  status VARCHAR(100) [NOTE: "สถานะการสั่งซื้อ."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงานที่ทำการสั่งซื้อ."]
  agent_id UUID [ref: > Agent.id, NOTE: "อ้างอิงถึงข้อมูลตัวแทนจำหน่าย."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Material Order Detail Management

**Description**: แสดงรายละเอียดวัสดุที่สั่งซื้อในแต่ละรายการ

| Column Name         | Data Type     | Constraints                             | Description                                               |
|---------------------|---------------|-----------------------------------------|-----------------------------------------------------------|
| `material_order_id` | `UUID`        | `REFERENCES MaterialOrder(id)`         | อ้างอิงถึงข้อมูลการสั่งซื้อวัสดุ.                        |
| `material_id`       | `UUID`        | `REFERENCES Material(id)`               | อ้างอิงถึงข้อมูลวัสดุ.                                   |
| `qty`               | `INT`         |                                         | จำนวนวัสดุที่สั่งซื้อ.                                   |
| `price`             | `DECIMAL(10, 2)` |                                     | ราคาแต่ละหน่วยของวัสดุ.                                 |
| `created_at`        | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was created.                   |
| `updated_at`        | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was last updated.              |

**Notes**:
- `material_order_id`: อ้างอิงถึงข้อมูลการสั่งซื้อวัสดุ.
- `material_id`: อ้างอิงถึงข้อมูลวัสดุ.

```sql
Table MaterialOrderDetail [NOTE: "ข้อมูลรายละเอียดการสั่งซื้อวัสดุ แสดงรายละเอียดวัสดุที่สั่งซื้อในแต่ละรายการ"] {
  material_order_id UUID [ref: > MaterialOrder.id, NOTE: "อ้างอิงถึงข้อมูลการสั่งซื้อวัสดุ."]
  material_id UUID [ref: > Material.id, NOTE: "อ้างอิงถึงข้อมูลวัสดุ."]
  qty INT [NOTE: "จำนวนวัสดุที่สั่งซื้อ."]
  price DECIMAL(10, 2) [NOTE: "ราคาแต่ละหน่วยของวัสดุ."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Material Disbursement Management

**Description**: แสดงรายละเอียดการเบิกจ่ายวัสดุโดยพนักงาน

| Column Name       | Data Type     | Constraints                            | Description                                               |
|-------------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `id`              | `UUID`        | `PRIMARY KEY, UNIQUE`                 | รหัสตารางการเบิกจ่ายวัสดุที่ไม่ซ้ำกัน.                  |
| `date`            | `TIMESTAMP`   |                                        | วันที่เบิกจ่ายวัสดุ.                                   |
| `employee_id`     | `UUID`        | `REFERENCES Employee(id)`              | อ้างอิงถึงข้อมูลพนักงานที่ทำการเบิกจ่าย.               |
| `created_at`      | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`           | Timestamp when the record was created.                   |
| `updated_at`      | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`           | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสตารางการเบิกจ่ายวัสดุที่ไม่ซ้ำกัน.

```sql
Table MaterialDisburse [NOTE: "ตารางการเบิกจ่ายวัสดุ แสดงรายละเอียดการเบิกจ่ายวัสดุโดยพนักงาน"] {
  id UUID [pk, unique, NOTE: "รหัสตารางการเบิกจ่ายวัสดุที่ไม่ซ้ำกัน."]
  date TIMESTAMP [NOTE: "วันที่เบิกจ่ายวัสดุ."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงานที่ทำการเบิกจ่าย."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Material Disburse Detail Management

**Description**: รายละเอียดการเบิกจ่ายวัสดุ

| Column Name       | Data Type     | Constraints                            | Description                                               |
|-------------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `qty`             | `INT`         |                                        | จำนวนวัสดุที่เบิกจ่าย.                                   |
| `material_id`     | `UUID`        | `REFERENCES Material(id)`              | อ้างอิงถึงข้อมูลวัสดุที่เบิกจ่าย.                       |
| `employee_id`     | `UUID`        | `REFERENCES Employee(id)`              | อ้างอิงถึงข้อมูลพนักงานที่ทำการเบิกจ่าย.               |

**Notes**:
- `qty`: จำนวนวัสดุที่เบิกจ่าย.

```sql
Table MaterialDisburseDetail [NOTE: "รายละเอียดการเบิกจ่ายวัสดุ"] {
  qty INT [NOTE: "จำนวนวัสดุที่เบิกจ่าย."]
  material_id UUID [ref: > Material.id, NOTE: "อ้างอิงถึงข้อมูลวัสดุที่เบิกจ่าย."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงานที่ทำการเบิกจ่าย."]
}
```
## Agent Management

**Description**: ข้อมูลตัวแทนจำหน่าย แสดงรายละเอียดของตัวแทนจำหน่ายในระบบ

| Column Name     | Data Type     | Constraints                            | Description                                               |
|-----------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                 | รหัสประจำตัวตัวแทนจำหน่ายที่ไม่ซ้ำกัน.                   |
| `name`          | `VARCHAR(255)` |                                        | ชื่อตัวแทนจำหน่าย.                                     |
| `address`       | `VARCHAR(255)` |                                        | ที่อยู่ของตัวแทนจำหน่าย.                               |
| `phone`         | `VARCHAR(20)`  |                                        | เบอร์โทรศัพท์ของตัวแทนจำหน่าย.                         |
| `email`         | `VARCHAR(255)` |                                        | อีเมลของตัวแทนจำหน่าย.                                 |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was created.                   |
| `updated_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำตัวตัวแทนจำหน่ายที่ไม่ซ้ำกัน.

```sql
Table Agent [NOTE: "ข้อมูลตัวแทนจำหน่าย แสดงรายละเอียดของตัวแทนจำหน่ายในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำตัวตัวแทนจำหน่ายที่ไม่ซ้ำกัน."]
  name VARCHAR(255) [NOTE: "ชื่อตัวแทนจำหน่าย."]
  address VARCHAR(255) [NOTE: "ที่อยู่ของตัวแทนจำหน่าย."]
  phone VARCHAR(20) [NOTE: "เบอร์โทรศัพท์ของตัวแทนจำหน่าย."]
  email VARCHAR(255) [NOTE: "อีเมลของตัวแทนจำหน่าย."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Medicine Management

**Description**: ข้อมูลยา แสดงรายละเอียดของยาที่มีในระบบ

| Column Name     | Data Type     | Constraints                            | Description                                               |
|-----------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                 | รหัสประจำยาที่ไม่ซ้ำกัน.                                  |
| `name`          | `VARCHAR(255)` |                                        | ชื่อยา.                                                 |
| `detail`        | `TEXT`        |                                        | รายละเอียดยา.                                           |
| `dosage`        | `VARCHAR(100)` |                                        | ขนาดยา.                                               |
| `created_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was created.                   |
| `updated_at`    | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | Timestamp when the record was last updated.              |

**Notes**:
- `id`: รหัสประจำยาที่ไม่ซ้ำกัน.

```sql
Table Medicine [NOTE: "ข้อมูลยา แสดงรายละเอียดของยาที่มีในระบบ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำยาที่ไม่ซ้ำกัน."]
  name VARCHAR(255) [NOTE: "ชื่อยา."]
  detail TEXT [NOTE: "รายละเอียดยา."]
  dosage VARCHAR(100) [NOTE: "ขนาดยา."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was created."]
  updated_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the record was last updated."]
}
```

## Medicine Type Management

**Description**: ข้อมูลประเภทยา

| Column Name     | Data Type     | Constraints                            | Description                                               |
|-----------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                 | รหัสประจำข้อมูลประเภทยา.                                   |
| `name`          | `VARCHAR`     |                                        | ชื่อประเภทยา.                                          |
| `detail`        | `TEXT`        |                                        | รายละเอียดประเภทยา.                                     |
| `agent_id`      | `UUID`        | `REFERENCES Agent(id)`                | อ้างอิงถึงข้อมูลเอเย่นต์.                                |

**Notes**:
- `id`: รหัสประจำข้อมูลประเภทยา.

```sql
Table MedicineType [NOTE: "ข้อมูลประเภทยา"] {
  id UUID [pk, unique, NOTE: "รหัสประจำข้อมูลประเภทยา."]
  name VARCHAR [NOTE: "ชื่อประเภทยา."]
  detail TEXT [NOTE: "รายละเอียดประเภทยา."]
  agent_id UUID [ref: > Agent.id, NOTE: "อ้างอิงถึงข้อมูลเอเย่นต์."]
}
```

## Medicine Order Management

**Description**: ข้อมูลการสั่งซื้อยา

| Column Name     | Data Type     | Constraints                            | Description                                               |
|-----------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                 | รหัสประจำข้อมูลการสั่งซื้อยา.                            |
| `date`          | `TIMESTAMP`   |                                        | วันที่สั่งซื้อ.                                          |
| `total_price`   | `DECIMAL`     |                                        | ราคารวม.                                                |
| `receive_date`  | `TIMESTAMP`   |                                        | วันที่รับ.                                              |
| `status`        | `VARCHAR`     |                                        | สถานะการสั่งซื้อ.                                      |
| `employee_id`   | `UUID`        | `REFERENCES Employee(id)`             | อ้างอิงถึงข้อมูลพนักงานที่ทำการสั่งซื้อ.                  |
| `agent_id`      | `UUID`        | `REFERENCES Agent(id)`                | อ้างอิงถึงข้อมูลตัวแทนจำหน่าย.                           |

**Notes**:
- `id`: รหัสประจำข้อมูลการสั่งซื้อยา.

```sql
Table MedicineOrder [NOTE: "ข้อมูลการสั่งซื้อยา"] {
  id UUID [pk, unique, NOTE: "รหัสประจำข้อมูลการสั่งซื้อยา."]
  date TIMESTAMP [NOTE: "วันที่สั่งซื้อ."]
  total_price DECIMAL [NOTE: "ราคารวม."]
  receive_date TIMESTAMP [NOTE: "วันที่รับ."]
  status VARCHAR [NOTE: "สถานะการสั่งซื้อ."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงานที่ทำการสั่งซื้อ."]
  agent_id UUID [ref: > Agent.id, NOTE: "อ้างอิงถึงข้อมูลตัวแทนจำหน่าย."]
}
```

## Medicine Order Detail Management

**Description**: ข้อมูลรายละเอียดการสั่งซื้อยา

| Column Name         | Data Type     | Constraints                            | Description                                               |
|---------------------|---------------|----------------------------------------|-----------------------------------------------------------|
| `medicine_order_id` | `UUID`        | `REFERENCES MedicineOrder(id)`        | อ้างอิงถึงข้อมูลการสั่งซื้อยา.                           |
| `medicine_id`       | `UUID`        | `REFERENCES Medicine(id)`              | อ้างอิงถึงข้อมูลยา.                                     |
| `price`             | `DECIMAL`     |                                        | ราคายา.                                                |
| `qty`               | `INT`         |                                        | จำนวนที่สั่งซื้อ.                                      |
| `remain`            | `INT`         |                                        | จำนวนค้างรับ.                                          |

**Notes**:
- `medicine_order_id`: อ้างอิงถึงข้อมูลการสั่งซื้อยา.

```sql
Table MedicineOrderDetail [NOTE: "ข้อมูลรายละเอียดการสั่งซื้อยา"] {
  medicine_order_id UUID [ref: > MedicineOrder.id, NOTE: "อ้างอิงถึงข้อมูลการสั่งซื้อยา."]
  medicine_id UUID [ref: > Medicine.id, NOTE: "อ้างอิงถึงข้อมูลยา."]
  price DECIMAL [NOTE: "ราคายา."]
  qty INT [NOTE: "จำนวนที่สั่งซื้อ."]
  remain INT [NOTE: "จำนวนค้างรับ."]
}
```

## Medicine Stock Management

**Description**: ข้อมูลสต๊อกหรือยาคงเหลือ

| Column Name     | Data Type     | Constraints                             | Description                                            |
|-----------------|---------------|-----------------------------------------|--------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                  | รหัสประจำข้อมูลสต๊อก.                                |
| `medicine_id`   | `UUID`        | `REFERENCES Medicine(id)`               | อ้างอิงถึงข้อมูลยา.                                  |
| `qty`           | `INT`         |                                         | จำนวนยาคงเหลือ.                                     |
| `expired_date`  | `DATE`        |                                         | วันหมดอายุของยา.                                   |

**Notes**:
- `id`: รหัสประจำข้อมูลสต๊อก.

```sql
Table MedicineStock [NOTE: "ข้อมูลสต๊อกหรือยาคงเหลือ"] {
  id UUID [pk, unique, NOTE: "รหัสประจำข้อมูลสต๊อก."]
  medicine_id UUID [ref: > Medicine.id, NOTE: "อ้างอิงถึงข้อมูลยา."]
  qty INT [NOTE: "จำนวนยาคงเหลือ."]
  expired_date DATE [NOTE: "วันหมดอายุของยา."]
}
```

## Prescription Table

**Description**: ตารางสำหรับข้อมูลการสั่งจ่ายยา

| Column Name      | Data Type     | Constraints                        | Description                                   |
|-------------------|---------------|------------------------------------|-----------------------------------------------|
| `id`              | `UUID`        | `PRIMARY KEY`, `UNIQUE`           | รหัสการสั่งจ่ายยาที่ไม่ซ้ำกัน.                 |
| `patient_id`      | `UUID`        | `REFERENCES Patient(id)`           | อ้างอิงถึงข้อมูลคนไข้.                        |
| `doctor_id`       | `UUID`        | `REFERENCES Employee(id)`          | อ้างอิงถึงข้อมูลแพทย์.                        |
| `course_id`       | `UUID`        | `REFERENCES Course(id)`            | อ้างอิงถึงข้อมูลการรักษา.                      |
| `date`            | `TIMESTAMP`   |                                    | วันที่สั่งจ่ายยา.                             |
| `instructions`     | `TEXT`        |                                    | คำแนะนำการใช้ยา.                             |

**Notes**:
- `id`: รหัสการสั่งจ่ายยาที่ไม่ซ้ำกัน.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `doctor_id`: อ้างอิงถึงข้อมูลแพทย์.
- `course_id`: อ้างอิงถึงข้อมูลการรักษา.
- `date`: วันที่สั่งจ่ายยา.
- `instructions`: คำแนะนำการใช้ยา.

```sql
Table Prescription [NOTE: "ข้อมูลการสั่งจ่ายยา"] {
  id UUID [pk, unique, NOTE: "รหัสการสั่งจ่ายยาที่ไม่ซ้ำกัน."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  doctor_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลแพทย์."]
  course_id UUID [ref: > Course.id, NOTE: "อ้างอิงถึงข้อมูลการรักษา."]
  date TIMESTAMP [NOTE: "วันที่สั่งจ่ายยา."]
  instructions TEXT [NOTE: "คำแนะนำการใช้ยา."]
}
```

## Medicine Disburse Management

**Description**: ข้อมูลการจ่ายยา

| Column Name     | Data Type     | Constraints                             | Description                                            |
|-----------------|---------------|-----------------------------------------|--------------------------------------------------------|
| `id`            | `UUID`        | `PRIMARY KEY, UNIQUE`                  | รหัสประจำข้อมูลการจ่ายยา.                            |
| `prescription_id`     | `UUID`        | `REFERENCES Prescription(id)`                | อ้างอิงถึงข้อมูลการรักษา.                            |
| `date`          | `TIMESTAMP`   |                                         | วันที่จ่ายยา.                                        |

**Notes**:
- `id`: รหัสประจำข้อมูลการจ่ายยา.

```sql
Table MedicineDisburse [NOTE: "ข้อมูลการจ่ายยา"] {
  id UUID [pk, unique, NOTE: "รหัสประจำข้อมูลการจ่ายยา."]
  prescription_id UUID [ref: > Prescription.id, NOTE: "อ้างอิงถึงข้อมูลการสั่งจ่ายยา."]
  date TIMESTAMP [NOTE: "วันที่จ่ายยา."]
}
```

## Medicine Disburse Detail Management

**Description**: ข้อมูลรายละเอียดการจ่ายยา

| Column Name             | Data Type     | Constraints                            | Description                                           |
|-------------------------|---------------|----------------------------------------|-------------------------------------------------------|
| `medicine_disburse_id`  | `UUID`        | `REFERENCES MedicineDisburse(id)`    | อ้างอิงถึงข้อมูลการจ่ายยา.                           |
| `medicine_stock_id`     | `UUID`        | `REFERENCES MedicineStock(id)`        | อ้างอิงถึงข้อมูลสต๊อกยา.                             |
| `price`                 | `DECIMAL`     |                                        | ราคายาที่ขาย.                                       |
| `unit`                  | `VARCHAR`     |                                        | หน่วยนับ.                                          |
| `qty`                   | `INT`         |                                        | จำนวนที่จ่าย.                                       |
| `dosage`                | `VARCHAR`     |                                        | ขนาดที่รับประทาน.                                  |
| `admin_method`          | `VARCHAR`     |                                        | วิธีการรับประทาน.                                  |
| `apply_method`          | `VARCHAR`     |                                        | วิธีการทายา.                                       |
| `time_of_admin`         | `TIMESTAMP`   |                                        | เวลาใช้ยา.                                         |

**Notes**:
- `medicine_disburse_id`: อ้างอิงถึงข้อมูลการจ่ายยา.
- `medicine_stock_id`: อ้างอิงถึงข้อมูลสต๊อกยา.

```sql
Table MedicineDisburseDetail [NOTE: "ข้อมูลรายละเอียดการจ่ายยา"] {
  medicine_disburse_id UUID [ref: > MedicineDisburse.id, NOTE: "อ้างอิงถึงข้อมูลการจ่ายยา."]
  medicine_stock_id UUID [ref: > MedicineStock.id, NOTE: "อ้างอิงถึงข้อมูลสต๊อกยา."]
  price DECIMAL [NOTE: "ราคายาที่ขาย."]
  unit VARCHAR [NOTE: "หน่วยนับ."]
  qty INT [NOTE: "จำนวนที่จ่าย."]
  dosage VARCHAR [NOTE: "ขนาดที่รับประทาน."]
  admin_method VARCHAR [NOTE: "วิธีการรับประทาน."]
  apply_method VARCHAR [NOTE: "วิธีการทายา."]
  time_of_admin TIMESTAMP [NOTE: "เวลาใช้ยา."]
}
```

## Course Management

**Description**: ข้อมูลคอร์สหรือการรักษา

| Column Name             | Data Type     | Constraints                            | Description                                           |
|-------------------------|---------------|----------------------------------------|-------------------------------------------------------|
| `id`                    | `UUID`        | `PRIMARY KEY`, `UNIQUE`                | รหัสประจำข้อมูลการรักษา.                           |
| `date`                  | `TIMESTAMP`   |                                        | วันที่รับการรักษา.                                   |
| `weight`                | `DECIMAL`     |                                        | น้ำหนักของคนไข้.                                   |
| `height`                | `DECIMAL`     |                                        | ส่วนสูงของคนไข้.                                   |
| `systolic`              | `INT`         |                                        | ความดันช่วงบน.                                     |
| `diastolic`             | `INT`         |                                        | ความดันช่วงล่าง.                                   |
| `heart_rate`            | `INT`         |                                        | อัตราการเต้นของหัวใจ.                             |
| `diagnose`              | `TEXT`        |                                        | การวินิจฉัย.                                       |
| `total_price`           | `DECIMAL`     |                                        | ราคารักษา.                                         |
| `status`                | `VARCHAR`     |                                        | สถานะการรักษา.                                     |
| `patient_id`            | `UUID`        | `REFERENCES Patient(id)`               | อ้างอิงถึงข้อมูลคนไข้.                             |
| `employee_id`           | `UUID`        | `REFERENCES Employee(id)`              | อ้างอิงถึงข้อมูลพนักงาน.                           |

**Notes**:
- `id`: รหัสประจำข้อมูลการรักษา.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `employee_id`: อ้างอิงถึงข้อมูลพนักงาน.

```sql
Table Course [NOTE: "ข้อมูลคอร์สหรือการรักษา"] {
  id UUID [pk, unique, NOTE: "รหัสประจำข้อมูลการรักษา."]
  date TIMESTAMP [NOTE: "วันที่รับการรักษา."]
  weight DECIMAL [NOTE: "น้ำหนักของคนไข้."]
  height DECIMAL [NOTE: "ส่วนสูงของคนไข้."]
  systolic INT [NOTE: "ความดันช่วงบน."]
  diastolic INT [NOTE: "ความดันช่วงล่าง."]
  heart_rate INT [NOTE: "อัตราการเต้นของหัวใจ."]
  diagnose TEXT [NOTE: "การวินิจฉัย."]
  total_price DECIMAL [NOTE: "ราคารักษา."]
  status VARCHAR [NOTE: "สถานะการรักษา."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงาน."]
}
```

## Receipt Management

**Description**: ใบเสร็จ

| Column Name                | Data Type     | Constraints                            | Description                                           |
|----------------------------|---------------|----------------------------------------|-------------------------------------------------------|
| `id`                       | `UUID`        | `PRIMARY KEY`, `UNIQUE`                | รหัสใบเสร็จ.                                       |
| `date`                     | `TIMESTAMP`   |                                        | วันที่ใบเสร็จ.                                     |
| `total_price`              | `DECIMAL`     |                                        | ราคารวมทั้งหมด ทั้งค่ารักษาและยา.                 |
| `course_id`                | `UUID`        | `REFERENCES Course(id)`                | อ้างอิงถึงข้อมูลการรักษา.                           |
| `medicine_disburse_id`     | `UUID`        | `REFERENCES MedicineDisburse(id)`     | อ้างอิงถึงข้อมูลการจ่ายยา.                         |
| `patient_id`               | `UUID`        | `REFERENCES Patient(id)`               | อ้างอิงถึงข้อมูลคนไข้.                             |
| `employee_id`              | `UUID`        | `REFERENCES Employee(id)`              | อ้างอิงถึงข้อมูลพนักงาน.                           |

**Notes**:
- `id`: รหัสใบเสร็จ.
- `course_id`: อ้างอิงถึงข้อมูลการรักษา.
- `medicine_disburse_id`: อ้างอิงถึงข้อมูลการจ่ายยา.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `employee_id`: อ้างอิงถึงข้อมูลพนักงาน.

```sql
Table Receipt [NOTE: "ใบเสร็จ"] {
  id UUID [pk, unique, NOTE: "รหัสใบเสร็จ."]
  date TIMESTAMP [NOTE: "วันที่ใบเสร็จ."]
  total_price DECIMAL [NOTE: "ราคารวมทั้งหมด ทั้งค่ารักษาและยา."]
  course_id UUID [ref: > Course.id, NOTE: "อ้างอิงถึงข้อมูลการรักษา."]
  medicine_disburse_id UUID [ref: > MedicineDisburse.id, NOTE: "อ้างอิงถึงข้อมูลการจ่ายยา."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  employee_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลพนักงาน."]
}
```

## Email Log Management

**Description**: ตารางการบันทึกอีเมลที่ส่งให้คนไข้

| Column Name            | Data Type     | Constraints                            | Description                                       |
|------------------------|---------------|----------------------------------------|---------------------------------------------------|
| `id`                   | `UUID`        | `PRIMARY KEY`, `UNIQUE`                | รหัสประจำการบันทึกอีเมลที่ไม่ซ้ำกัน.             |
| `patient_id`           | `UUID`        | `REFERENCES Patient(id)`               | อ้างอิงถึงข้อมูลคนไข้.                           |
| `email`                | `VARCHAR(255)`|                                        | อีเมลที่ส่งไปยังคนไข้.                           |
| `subject`              | `VARCHAR(255)`|                                        | หัวข้อของอีเมล.                                 |
| `body`                 | `TEXT`        |                                        | เนื้อหาของอีเมล.                                 |
| `sent_at`             | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`            | วันที่และเวลาที่ส่งอีเมล.                        |
| `status`               | `VARCHAR(50)` |                                        | สถานะการส่งอีเมล (เช่น "Sent", "Failed").       |

**Notes**:
- `id`: รหัสประจำการบันทึกอีเมลที่ไม่ซ้ำกัน.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `sent_at`: วันที่และเวลาที่ส่งอีเมล.

```sql
Table EmailLog [NOTE: "ตารางการบันทึกอีเมลที่ส่งให้คนไข้"] {
  id UUID [pk, unique, NOTE: "รหัสประจำการบันทึกอีเมลที่ไม่ซ้ำกัน."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  email VARCHAR(255) [NOTE: "อีเมลที่ส่งไปยังคนไข้."]
  subject VARCHAR(255) [NOTE: "หัวข้อของอีเมล."]
  body TEXT [NOTE: "เนื้อหาของอีเมล."]
  sent_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "วันที่และเวลาที่ส่งอีเมล."]
  status VARCHAR(50) [NOTE: "สถานะการส่งอีเมล (เช่น 'Sent', 'Failed')."]
}

```


## Database Movement Log

**Description**: ตารางการบันทึกการเคลื่อนไหวของฐานข้อมูลเพื่อการตรวจสอบและติดตาม

| Column Name            | Data Type     | Constraints                            | Description                                       |
|------------------------|---------------|----------------------------------------|---------------------------------------------------|
| `id`                   | `UUID`        | `PRIMARY KEY`, `UNIQUE`               | รหัสประจำการบันทึกการเคลื่อนไหวที่ไม่ซ้ำกัน.     |
| `table_name`           | `VARCHAR(255)`|                                        | ชื่อของตารางที่มีการเคลื่อนไหว.                  |
| `operation`            | `VARCHAR(50)` |                                        | ประเภทของการดำเนินการ (เช่น "INSERT", "UPDATE", "DELETE"). |
| `record_id`            | `UUID`        |                                        | รหัสประจำเรคคอร์ดที่ถูกเปลี่ยนแปลง.               |
| `changed_data`         | `JSON`        |                                        | ข้อมูลที่ถูกเปลี่ยนแปลงในรูปแบบ JSON.            |
| `changed_at`           | `TIMESTAMP`   | `DEFAULT CURRENT_TIMESTAMP`           | วันที่และเวลาที่มีการเคลื่อนไหว.                  |
| `user_id`              | `UUID`        | `REFERENCES User(id)`                 | อ้างอิงถึงข้อมูลผู้ใช้ที่ทำการเคลื่อนไหว.          |

**Notes**:
- `id`: รหัสประจำการบันทึกการเคลื่อนไหวที่ไม่ซ้ำกัน.
- `table_name`: ชื่อของตารางที่มีการเคลื่อนไหว.
- `operation`: ประเภทของการดำเนินการที่กระทำต่อเรคคอร์ด.
- `record_id`: รหัสประจำเรคคอร์ดที่ถูกเปลี่ยนแปลง.
- `changed_data`: รายละเอียดข้อมูลที่ถูกเปลี่ยนแปลง.

```sql
Table DatabaseMovementLog [NOTE: "ตารางการบันทึกการเคลื่อนไหวของฐานข้อมูลเพื่อการตรวจสอบและติดตาม"] {
  id UUID [pk, unique, NOTE: "รหัสประจำการบันทึกการเคลื่อนไหวที่ไม่ซ้ำกัน."]
  table_name VARCHAR(255) [NOTE: "ชื่อของตารางที่มีการเคลื่อนไหว."]
  operation VARCHAR(50) [NOTE: "ประเภทของการดำเนินการ (เช่น 'INSERT', 'UPDATE', 'DELETE')."]
  record_id UUID [NOTE: "รหัสประจำเรคคอร์ดที่ถูกเปลี่ยนแปลง."]
  changed_data JSON [NOTE: "ข้อมูลที่ถูกเปลี่ยนแปลงในรูปแบบ JSON."]
  changed_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "วันที่และเวลาที่มีการเคลื่อนไหว."]
  user_id UUID [ref: > User.id, NOTE: "อ้างอิงถึงข้อมูลผู้ใช้ที่ทำการเคลื่อนไหว."]
}
```


## Feedback Table

**Description**: ตารางสำหรับการบันทึกข้อเสนอแนะแพทย์จากคนไข้

| Column Name     | Data Type | Constraints                        | Description                                   |
|------------------|-----------|------------------------------------|-----------------------------------------------|
| `id`             | `UUID`    | `PRIMARY KEY`, `UNIQUE`           | รหัสข้อเสนอแน่ที่ไม่ซ้ำกัน.                    |
| `patient_id`     | `UUID`    | `REFERENCES Patient(id)`           | อ้างอิงถึงข้อมูลคนไข้.                        |
| `feedback_text`  | `TEXT`    |                                    | ข้อความข้อเสนอแน.                             |
| `created_at`     | `TIMESTAMP`| `DEFAULT CURRENT_TIMESTAMP`       | Timestamp when the feedback was created.     |

**Notes**:
- `id`: รหัสข้อเสนอแน่ที่ไม่ซ้ำกัน.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `feedback_text`: ข้อความข้อเสนอแน.
- `created_at`: วันที่และเวลาที่มีการบันทึกข้อเสนอแนะแพทย์.

```sql
Table Feedback [NOTE: "ตารางสำหรับการบันทึกข้อเสนอแนะแพทย์จากคนไข้"] {
  id UUID [pk, unique, NOTE: "รหัสข้อเสนอแน่ที่ไม่ซ้ำกัน."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  feedback_text TEXT [NOTE: "ข้อความข้อเสนอแน."]
  created_at TIMESTAMP [default: `CURRENT_TIMESTAMP`, NOTE: "Timestamp when the feedback was created."]
}
```


## Insurance Table

**Description**: ตารางสำหรับข้อมูลประกันสุขภาพ

| Column Name      | Data Type     | Constraints                        | Description                                   |
|-------------------|---------------|------------------------------------|-----------------------------------------------|
| `id`              | `UUID`        | `PRIMARY KEY`, `UNIQUE`           | รหัสประกันสุขภาพที่ไม่ซ้ำกัน.                 |
| `patient_id`      | `UUID`        | `REFERENCES Patient(id)`           | อ้างอิงถึงข้อมูลคนไข้.                        |
| `provider`        | `VARCHAR(255)`|                                    | ชื่อบริษัทประกันภัย.                          |
| `policy_number`   | `VARCHAR(100)`|                                    | หมายเลขกรมธรรม์.                             |
| `valid_until`     | `DATE`        |                                    | วันหมดอายุของกรมธรรม์.                       |

**Notes**:
- `id`: รหัสประกันสุขภาพที่ไม่ซ้ำกัน.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `provider`: ชื่อบริษัทประกันภัย.
- `policy_number`: หมายเลขกรมธรรม์.
- `valid_until`: วันหมดอายุของกรมธรรม์.

```sql
Table Insurance [NOTE: "ข้อมูลประกันสุขภาพ"] {
  id UUID [pk, unique, NOTE: "รหัสประกันสุขภาพที่ไม่ซ้ำกัน."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  provider VARCHAR(255) [NOTE: "ชื่อบริษัทประกันภัย."]
  policy_number VARCHAR(100) [NOTE: "หมายเลขกรมธรรม์."]
  valid_until DATE [NOTE: "วันหมดอายุของกรมธรรม์."]
}
```

## Referral Table

**Description**: ตารางสำหรับข้อมูลการส่งต่อ

| Column Name           | Data Type     | Constraints                        | Description                                   |
|------------------------|---------------|------------------------------------|-----------------------------------------------|
| `id`                   | `UUID`        | `PRIMARY KEY`, `UNIQUE`           | รหัสการส่งต่อที่ไม่ซ้ำกัน.                     |
| `patient_id`           | `UUID`        | `REFERENCES Patient(id)`           | อ้างอิงถึงข้อมูลคนไข้.                        |
| `referred_doctor_id`   | `UUID`        | `REFERENCES Employee(id)`          | อ้างอิงถึงข้อมูลแพทย์ที่ถูกส่งต่อ.             |
| `reason`               | `TEXT`        |                                    | เหตุผลในการส่งต่อ.                           |
| `referral_date`        | `TIMESTAMP`   |                                    | วันที่ส่งต่อ.                                 |

**Notes**:
- `id`: รหัสการส่งต่อที่ไม่ซ้ำกัน.
- `patient_id`: อ้างอิงถึงข้อมูลคนไข้.
- `referred_doctor_id`: อ้างอิงถึงข้อมูลแพทย์ที่ถูกส่งต่อ.
- `reason`: เหตุผลในการส่งต่อ.
- `referral_date`: วันที่ส่งต่อ.

```sql
Table Referral [NOTE: "ข้อมูลการส่งต่อ"] {
  id UUID [pk, unique, NOTE: "รหัสการส่งต่อที่ไม่ซ้ำกัน."]
  patient_id UUID [ref: > Patient.id, NOTE: "อ้างอิงถึงข้อมูลคนไข้."]
  referred_doctor_id UUID [ref: > Employee.id, NOTE: "อ้างอิงถึงข้อมูลแพทย์ที่ถูกส่งต่อ."]
  reason TEXT [NOTE: "เหตุผลในการส่งต่อ."]
  referral_date TIMESTAMP [NOTE: "วันที่ส่งต่อ."]
}
```