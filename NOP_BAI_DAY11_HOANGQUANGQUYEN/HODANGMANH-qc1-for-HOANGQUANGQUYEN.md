# Phiếu QC 1 — Road v1.0

- Lô được kiểm: Hoàng Quảng Quyền (2A202603082)
- Người kiểm: Hồ Đăng Mạnh (2A202603092)
- Ngày kiểm: 22/11/2026
- Phiên bản guideline: Road v1.0
- File được kiểm: `out/core_review/front-prelabel-core.zip` và `out/core_review/fisheye-prelabel-core.zip`. Đây là bản rà soát nhãn sơ bộ, chưa có manifest ghi `revision`.

| ZIP | SHA-256 |
| --- | --- |
| `front-prelabel-core.zip` | `d9129de00ba666dd20b6b84c2bc8eff55fa4c6bc56a08f8e0a9068e60bee0e71` |
| `fisheye-prelabel-core.zip` | `fd0797bc50407b64ce7c94160144c6408397a75d9cdb37ebce96c34b09c36147` |

**Mẫu kiểm gồm 6 ảnh bắt buộc và 0 ảnh thêm.** Chọn ba ảnh camera trước và ba ảnh fisheye từ các góc trước, sau và bên trái. Đối chiếu ảnh gốc với hình và thuộc tính trong XML.

| Ảnh | Shape trong ZIP | Tag trong ZIP | Tổng nhãn đã kiểm |
| --- | ---: | ---: | ---: |
| A01 | 4 | 4 | 8 |
| A03 | 6 | 4 | 10 |
| A07 | 6 | 4 | 10 |
| B02 | 0 | 4 | 4 |
| B03 | 0 | 4 | 4 |
| B05 | 0 | 4 | 4 |
| **Tổng** | **16** | **24** | **40** |

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 5 | 5 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 3 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 5 | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 3 | 3 | chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 1 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 2 | 2 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 3 | 1 | chính |
| QC1-12 file | lỗi file | 42 | 21 | nhẹ |

`QC1-01` kiểm sự hiện diện của 24 tag và giá trị camera của cả sáu ảnh. `QC1-02` kiểm năm vạch sát xe thấy được trong ba ảnh A. `QC1-03` đến `QC1-06` rà 12 polyline lane. `QC1-07` kiểm ba polygon drivable có sẵn và hai đối tượng cần có ở B05. `QC1-08` kiểm một đèn đã gán và hai cụm đèn lớn nhìn thấy ở B02. `QC1-09` rà đèn đã gán ở A03. `QC1-10` ghi hai biển rõ trong A03. `QC1-11` rà ba ảnh fisheye. `QC1-12` kiểm hai ZIP và 40 nhãn trong mẫu.

Thuộc tính trống được ghi ở `QC1-12`, mỗi nhãn một dòng. 12 lane đều có `style`, `color`, `kind` trống và đèn A03 thiếu `type`, `facing`. Vì vậy số 0 ở `QC1-06` và `QC1-09` chỉ là số lỗi riêng của các mã đó. `QC1-02` ghi riêng vạch sát xe thấy được nhưng chưa có nhãn mang `position` tương ứng. Hai ZIP đọc được, chỉ chứa `annotations.xml`. Camera đúng ở cả sáu ảnh.

## Danh sách lỗi

ID hình là thứ tự shape trong XML của từng ảnh, bắt đầu từ 0. Tọa độ sau `@` là điểm đầu của hình, tính theo pixel ảnh gốc. Với nhãn bị bỏ sót, tọa độ trong mô tả chỉ vị trí gần đúng để tìm trên ảnh.

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A01 | `lane#2@(105,717)` · L1 | nặng | Vạch đứt trắng sát trái thấy rõ. Polyline đã có, cần đặt `position=L1`. |
| 2 | QC1-02 | A01 | `lane#1@(716,717)` · R1 | nặng | Vạch đứt trắng sát phải thấy trên mặt đường. Polyline đã có, cần đặt `position=R1` sau khi rà tâm vạch. |
| 3 | QC1-02 | A03 | `lane#1@(199,699)` · L1 | nặng | Vạch vàng sát trái làn xe thấy rõ. Polyline đã có, cần đặt `position=L1`. |
| 4 | QC1-02 | A03 | `lane#2@(933,647)` · R1 | nặng | Có vệt trắng đứt sát phải, gần chữ `SCHOOL`. Cần sửa điểm rồi đặt `position=R1`. |
| 5 | QC1-02 | A07 | `lane#5@(771,557)` · R1 | nặng | Vạch trắng liền sát phải xe thấy rõ. Polyline đã có, cần đặt `position=R1`. |
| 6 | QC1-03 | A03 | `lane#3@(221,525)` | nặng | Polyline giữa ảnh đi dọc mép gờ bê tông của dải phân cách. Bỏ nhãn `lane` trên đoạn này. |
| 7 | QC1-03 | A03 | `lane#4@(1,625)` | nặng | Đoạn gần xe nối vào `lane#3` trên cùng mép gờ bê tông. Bỏ nhãn `lane` trên đoạn này. |
| 8 | QC1-03 | A07 | `lane#3@(0,532)` | nặng | Polyline bám chân dải chắn bê tông bên trái, ở chỗ không có vạch sơn. |
| 9 | QC1-04 | A01 | `lane#3@(1,607)` | chính | Vạch trắng đôi bên trái vẫn thấy sau điểm cuối `(222,528)`. Kéo điểm đến đoạn xa nhất còn thấy và rà lại tâm vạch. |
| 10 | QC1-04 | A03 | `lane#2@(933,647)` | chính | Đầu gần xe kéo tới `(933,647)`, vượt xuống vùng nhựa không thấy vệt trắng. Đặt điểm bám vệt sơn còn nhìn được gần chữ `SCHOOL`. |
| 11 | QC1-07 | A01 | `drivable#0@(0,561)` | chính | Polygon vượt qua vạch vàng bên phải vào lề, rõ gần `(1262,633)`. Cắt vùng theo ranh giới phần xe chạy. |
| 12 | QC1-07 | A07 | `drivable#1@(757,555)` | chính | Polygon cắt ngang làn sát sau ô tô bạc, quanh `y=420`. Rà vùng `direct` theo mặt đường xe đi được khi trống. |
| 13 | QC1-07 | B05 | `crosswalk` · thiếu | chính | Thiếu polygon bao vạch qua đường ngay sát thân xe, trải từ giữa trái sang phải. |
| 14 | QC1-07 | B05 | `road_curb` · thiếu | chính | Thiếu polyline theo mép vỉa hè cong phía trên các vạch qua đường. |
| 15 | QC1-08 | A03 | `traffic_light#5@(708,312)` | chính | Đèn trong hộp sáng xanh gần `(712,321)` nhưng `color=unknown`. Sửa thành `green`. Cần xác nhận hướng để chốt mức lỗi. |
| 16 | QC1-08 | B02 | `traffic_light` · thiếu, góc trên trái | chính | Thiếu box cụm đèn sát viền quanh `(121,149)`, cao hơn 8 px. Rà `edge_zone` khi thêm box. |
| 17 | QC1-08 | B02 | `traffic_light` · thiếu, góc trên phải | chính | Thiếu box cụm đèn sát viền cạnh người đi bộ, quanh `(1115,113)`, cao hơn 8 px. Rà `edge_zone` khi thêm box. |
| 18 | QC1-10 | A03 | `traffic_sign` · thiếu | chính | Biển cảnh báo vàng bên phải, trên xe tải trắng, quanh `(1020,310)`, không có box. |
| 19 | QC1-10 | A03 | `traffic_sign` · thiếu | chính | Biển công trường hình thoi màu cam quanh `(812,329)` không có box. |
| 20 | QC1-11 | B03 | `lane` · thiếu | chính | Ảnh camera sau có vạch trắng đứt rõ phía phải ảnh, qua các đoạn gần `(773,350)` và `(925,595)`. XML chỉ có tag, thiếu polyline dọc cung vạch. |
| 21 | QC1-12 | A01 | `drivable#0@(0,561)` | nhẹ | `area_type` trống. |
| 22 | QC1-12 | A01 | `lane#1@(716,717)` | nhẹ | `style`, `color`, `kind` trống. |
| 23 | QC1-12 | A01 | `lane#2@(105,717)` | nhẹ | `style`, `color`, `kind` trống. |
| 24 | QC1-12 | A01 | `lane#3@(1,607)` | nhẹ | `position`, `style`, `color`, `kind` trống. |
| 25 | QC1-12 | A03 | `lane#0@(1278,587)` | nhẹ | `position`, `style`, `color`, `kind` trống. |
| 26 | QC1-12 | A03 | `lane#1@(199,699)` | nhẹ | `style`, `color`, `kind` trống. |
| 27 | QC1-12 | A03 | `lane#2@(933,647)` | nhẹ | `style`, `color`, `kind` trống. |
| 28 | QC1-12 | A03 | `lane#3@(221,525)` | nhẹ | `position`, `style`, `color`, `kind` trống trên hình hiện tại. |
| 29 | QC1-12 | A03 | `lane#4@(1,625)` | nhẹ | `position`, `style`, `color`, `kind` trống trên hình hiện tại. |
| 30 | QC1-12 | A03 | `traffic_light#5@(708,312)` | nhẹ | `type`, `facing` trống. |
| 31 | QC1-12 | A03 | `tag:timeofday` | nhẹ | `value` trống. |
| 32 | QC1-12 | A03 | `tag:weather` | nhẹ | `value` trống. |
| 33 | QC1-12 | A07 | `drivable#0@(699,276)` | nhẹ | `area_type` trống. |
| 34 | QC1-12 | A07 | `drivable#1@(757,555)` | nhẹ | `area_type` trống. |
| 35 | QC1-12 | A07 | `lane#2@(1277,488)` | nhẹ | `position`, `style`, `color`, `kind` trống. |
| 36 | QC1-12 | A07 | `lane#3@(0,532)` | nhẹ | `position`, `style`, `color`, `kind` trống trên hình hiện tại. |
| 37 | QC1-12 | A07 | `lane#4@(997,549)` | nhẹ | `position`, `style`, `color`, `kind` trống. |
| 38 | QC1-12 | A07 | `lane#5@(771,557)` | nhẹ | `style`, `color`, `kind` trống. |
| 39 | QC1-12 | A07 | `tag:weather` | nhẹ | `value` trống. |
| 40 | QC1-12 | B02 | `tag:weather` | nhẹ | `value` trống. |
| 41 | QC1-12 | B05 | `tag:weather` | nhẹ | `value` trống. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp |
| --- | --- | --- |
| A03 | `traffic_light#5` quay về xe hay quay chéo? Nếu `facing=front`, lỗi màu chuyển sang mức nặng. | Chưa xác nhận. |
| A07 | Dải chắn bê tông che sát mép trái và không thấy sơn L1. Xác nhận miễn L1 cho ảnh này. | Chưa xác nhận. Chưa tính lỗi thiếu L1. |

Không có ảnh nào sạch lỗi trên toàn bộ 12 mục trong mẫu. Ba lỗi dễ đối chiếu lại là #5 (vạch phải A07), #15 (màu đèn A03) và #13 (vạch qua đường B05).

## Quyết định

- Lỗi nặng: **8**.
- Lỗi chính: **12 / 40 nhãn = 30%**.
- Lỗi nhẹ: **21**.
- Ca chờ lead: **2**.

**Rework** cho bản `core_review`. Mẫu có lỗi nặng và tỉ lệ lỗi chính vượt 5%. Cần gán đúng L1/R1 ở các ảnh A, sửa nhãn và thuộc tính đã liệt kê, bổ sung shape còn thiếu ở fisheye rồi kiểm lại trên bản export mới.

[Thang mức lỗi và luật quyết định QC 1](../docs/qc_severity_road_v1.0.md)
