[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572337&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** AI20K-0275
**Name:** Pham Xuan Khang
**Email:** phamxuankhang2004@gmail.com

---

## Mo ta

Bai lab nay xay dung mot ETL (Extract - Transform - Load) pipeline don gian bang Python de xu ly du lieu san pham tu file JSON. Pipeline bao gom 4 buoc chinh:

1. **Extract**: Doc du lieu thu so tu `raw_data.json`
2. **Validate**: Loai bo cac ban ghi khong hop le (gia <= 0, category rong)
3. **Transform**: Chuan hoa category sang Title Case, tinh gia sau giam 10%, them timestamp xu ly
4. **Load**: Luu ket qua sach vao `processed_data.csv`

Sau do, chay `agent_simulation.py` de quan sat su khac biet giua viec agent su dung du lieu sach (`processed_data.csv`) va du lieu "rac" (`garbage_data.csv`), qua do hieu ro tam quan trong cua data observability.

---

## Cach chay (How to Run)

### Prerequisites

```bash
pip install pandas
```

### Chay ETL Pipeline

```bash
python solution.py
```

Ket qua: file `processed_data.csv` se duoc tao ra voi 3 ban ghi hop le (2 ban ghi bi loai do gia am va category rong).

### Tao Garbage Data

```bash
python generate_garbage.py
```

Ket qua: file `garbage_data.csv` se duoc tao ra chua cac van de: duplicate ID, sai kieu du lieu, outlier cuc doan, null values.

### Chay Agent Simulation (Stress Test)

```bash
python agent_simulation.py
```

So sanh ket qua agent voi du lieu sach vs. du lieu rac:
- **Clean data**: Agent tra loi dung — Laptop $1200
- **Garbage data**: Agent tra loi sai — Nuclear Reactor $999999 (outlier)

### Chay Tests

```bash
pytest tests/test_autograder.py -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline chinh (Extract, Validate, Transform, Load)
├── agent_simulation.py      # RAG-like agent simulation
├── generate_garbage.py      # Script tao garbage_data.csv
├── raw_data.json            # Du lieu nguon (5 ban ghi, 2 ban ghi co loi co y)
├── processed_data.csv       # Output sau khi chay pipeline (3 ban ghi sach)
├── garbage_data.csv         # Du lieu rac de stress test agent
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

| Buoc | Chi tiet |
|------|----------|
| Raw records doc duoc | 5 |
| Records bi loai (validate) | 2 (id=3: gia -10; id=4: category rong) |
| Records hop le (saved) | 3 (Laptop, Chair, Monitor) |
| discounted_price | = price * 0.9 (giam 10%) |
| Category format | Title Case (vd: "electronics" -> "Electronics") |
| Agent (clean data) | Laptop at $1200 — chinh xac |
| Agent (garbage data) | Nuclear Reactor at $999999 — sai do outlier |

**Ket luan**: Chat luong du lieu (Data Quality) quan trong hon bat ky toi uu hoa nao khac. Garbage in = Garbage out.
