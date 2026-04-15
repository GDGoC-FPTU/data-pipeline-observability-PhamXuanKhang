# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600275
**Name:** Pham Xuan Khang
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 10 | Correct answer — Laptop la san pham electronics dat nhat trong tap du lieu sach |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Sai hoan toan — Nuclear Reactor la outlier bat thuong, gia tri $999999 khong phan anh thuc te |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi agent su dung bo du lieu garbage (`garbage_data.csv`), ket qua tra ve bi sai nghiem trong vi nhieu van de chat luong du lieu ton tai dong thoi. Thu nhat, bo du lieu chua outlier cuc doan: ban ghi "Nuclear Reactor" co gia tri $999999 — mot outlier bat hop ly khong the xay ra trong thuc te — khien agent lua chon no lam "best electronics" du day la mot gia tri sai lech hoan toan. Thu hai, co duplicate ID (ca hai ban ghi id=1 deu ton tai), gay ra su nham lan trong viec xac dinh san pham duy nhat. Thu ba, co ban ghi co gia tri sai kieu du lieu ("ten dollars" thay vi so), khien cac phep tinh so hoc co the gap loi hoac cho ket qua khong xac dinh. Cuoi cung, co null values o ca cot `id` lan `category`, tao ra ban ghi "ma" khong co y nghia nghiep vu. Tat ca nhung van de nay cho thay rang chat luong du lieu dau vao anh huong truc tiep den chat luong quyet dinh cua AI agent. Du logic cua agent co chinh xac den dau, neu du lieu bi "dau doc" thi ket qua dau ra se luon sai. Day la bai hoc cot loi cua data observability: garbage in, garbage out.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Du prompt cua agent duoc viet chinh xac va logic tim kiem san pham gia cao nhat la hop le, nhung khi du lieu dau vao chua outlier (Nuclear Reactor $999999), agent van tra ve ket qua sai. Dieu nay chung minh rang chat luong du lieu quan trong hon chat luong cau lenh. Mot pipeline ETL tot voi buoc validate va transform ky luong la nen tang bat buoc de bat ky he thong AI nao hoat dong dung dan va dang tin cay.
