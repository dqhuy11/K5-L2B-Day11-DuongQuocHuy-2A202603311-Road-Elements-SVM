# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đặng Trung Hiếu        Người kiểm (học viên): Dương Quốc Huy  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `dangtrunghieu-front.zip` (sha256 `5104cf5f…`), `dangtrunghieu-fisheye.zip` (sha256 `2c649c1b…`), `revision` 1  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 54  

Mẫu kiểm: A01–A06. Số nhãn: A01 9 shape + 4 tag · A02 7 + 4 · A03 4 + 4 · A04 4 + 4 · A05 1 + 4 · A06 5 + 4 = 54.  
Cột "Nhãn (label, id)": id là thứ tự của hình trong ảnh đó trong `annotations.xml`, đếm từ 0 (export CVAT 1.1 không ghi id của hình).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 (6 ảnh × 4 tag) | 3 | nhẹ (weather); tag camera đúng cả 6 ảnh |
| QC1-02 đủ L1, R1 | bỏ sót | 12 (6 ảnh × 2) | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 11 lane | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 11 lane | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 11 lane | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 11 lane | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 16 (15 drivable + 1 crosswalk cần có ở A06) | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 5 (4 đèn đã gán + 1 đèn thiếu, A06) | 1 | chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 5 (4 đèn + 1 biển, A06) | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 6 (A06: 1 đã gán + 3 thiếu; A01: 2, chờ lead) | 3 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 (mẫu không có ảnh fisheye) | 0 | chính |
| QC1-12 file | lỗi file | 2 file | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-06 | A01 | lane, #0 (R2) | chính | Vạch mép phải màu vàng nhưng `color = white`; đúng là `yellow` |
| 2 | QC1-07 | A01 | drivable, #8 | chính | Polygon `direct` nằm bên trái vạch mép L2, ngoài phần đường của chiều mình: sai `area_type` và tràn ra ngoài vạch mép |
| 3 | QC1-07 | A01 | drivable, #7 | chính | Polygon `alternative` phủ dải lề giữa vạch vàng R2 và lan can; lề không phải làn đi được |
| 4 | QC1-07 | A02 | drivable, #6 | chính | Polygon `alternative` bên phải R1 phủ lề sỏi cạnh đường ray; R1 là vạch mép, bên ngoài không phải làn |
| 5 | QC1-02 | A03 | lane (thiếu L1) | nặng | Thiếu vạch vàng liền ở mép trái làn đang đi (L1) |
| 6 | QC1-03 | A03 | lane, #2 | nặng | Vạch trắng đứt nằm bên phải làn đang đi (polygon direct #3 của chính bạn nằm bên trái nó) nhưng ghi `L1`; đúng là `R1` |
| 7 | QC1-03 | A03 | lane, #0 | nặng | Vạch đứt kế tiếp bên phải ghi `L2`; đúng là `R2` |
| 8 | QC1-04 | A04 | lane (thiếu R2) | chính | Thiếu vạch trắng liền ngăn làn xe đạp bên phải (R2), dù polygon alternative #1 đã dừng đúng ở vạch này |
| 9 | QC1-01 | A04 | tag weather | nhẹ | Trời phủ mây kín, đường khô: `weather = clear`, đề nghị `overcast` |
| 10 | QC1-01 | A05 | tag weather | nhẹ | Trời trắng đục, phủ mây kín: `weather = clear`, đề nghị `overcast` |
| 11 | QC1-09 | A06 | traffic_light, #0 | chính | Cụm đèn góc trên trái quay ngang (thấy cạnh vỏ, không thấy mặt đèn) nhưng `facing = front`; đúng là `side` |
| 12 | QC1-08 | A06 | traffic_light (thiếu) | chính | Thiếu đèn người đi bộ ngay dưới đèn #5 (khoảng x 945–965, y 338–366), đang sáng hình người đi; `type = pedestrian` |
| 13 | QC1-10 | A06 | traffic_sign (thiếu) | chính | Thiếu biển hình thoi màu cam giữa ảnh (khoảng x 561–593, y 305–334), `group = warning` |
| 14 | QC1-10 | A06 | traffic_sign (thiếu) | chính | Thiếu biển hình thoi màu vàng bên phải (khoảng x 855–898, y 319–363), `group = warning` |
| 15 | QC1-10 | A06 | traffic_sign (thiếu) | chính | Thiếu biển tên đường màu xanh lá (khoảng x 879–914, y 310–326, cao 16 px), `group = information` |
| 16 | QC1-07 | A06 | crosswalk (thiếu) | chính | Vạch ngựa vằn cắt ngang đường trước mặt (khoảng y 400–490) chưa gán crosswalk |
| 17 | QC1-01 | A06 | tag weather | nhẹ | Trời trắng đục, phủ mây kín: `weather = clear`, đề nghị `overcast` |

Lane #3 (L2) ở A01 có `kind = double`: mentor xác nhận đây là vạch đôi, nên không tính lỗi.

Ảnh trong mẫu không có lỗi nặng hoặc chính: **A05** (chỉ có lỗi nhẹ ở tag weather, dòng 10). Drivable `direct` dừng gần đúng ở bánh các xe đỗ hai bên; ảnh không có vạch nên không có lane, đúng với guideline.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A01 | Bảng kế hoạch của A01 có yêu cầu biển không? Có 2 biển xanh chỉ dẫn (cao > 8 px) chưa gán. Nếu có yêu cầu thì thêm 2 lỗi QC1-10 chính. | |
| A03 | Trọng tâm của slot là `occluded`, nhưng không polyline nào bật occluded. Tôi chưa xác định được đoạn vạch bị che, nên chưa tính lỗi QC1-05. | |
| A04 | Trời sáng đều nhưng xe đã bật đèn: `timeofday` nên là `dusk` (bạn chọn) hay `day`? Tôi chưa tính lỗi. | |
| A05 | Đường không có vạch: lint báo thiếu L1 và R1. Cần coach xác nhận để miễn QC1-02. Đường hai chiều không vạch thì `direct` là cả mặt đường (bạn chọn) hay nửa bên phải? | Coach: ảnh không có vạch, miễn QC1-02. Câu hỏi về `direct` chưa có lời đáp |
| A06 | Lint báo thiếu L1 và R1. Bên phải làn là hàng cột, không có vạch; bên trái chỉ thấy một đoạn vạch vàng ở xa. Cần coach xác nhận miễn QC1-02. Tôi chưa tính lỗi. | Coach: ảnh không có vạch, miễn QC1-02 |

Các câu hỏi trên không đổi kết luận (lô đã có lỗi nặng và tỉ lệ lỗi chính vượt 5 %), nên không cần Hold.

## Quyết định
Lỗi nặng: 3   Lỗi chính: 11 / 54 nhãn = 20,4 %   Lỗi nhẹ: 3   Ca chờ lead: 5 (không ảnh hưởng kết luận)  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn 3 lỗi nặng ở A03 (thiếu L1, sai `position` hai vạch); chỉ một lỗi nặng đã đủ Rework. Tỉ lệ lỗi chính 20,4 % cũng vượt ngưỡng 5 %.

## Ghi chú ngoài mẫu (không tính vào tỉ lệ, để bạn sửa luôn khi Rework)
- **Cả 8 ảnh fisheye (B01–B08) đều có `camera = front`.** Đúng là FV → `fisheye_front`, RV → `fisheye_rear`, MVL → `fisheye_left`, MVR → `fisheye_right`. `road_check lint` cũng báo 8 lỗi QC1-01 nặng.
- Lô fisheye chỉ có crosswalk: không có lane, drivable hay road_curb nào. B03 không có hình nào.
- A07: hai vạch bên phải làn đang đi ghi L1/L2, đúng là R1/R2 (cùng lỗi với A03). Drivable `direct` khoét quanh xe phía trước.
- A11 drivable #2 (bên phải R1) ghi `direct`; đúng là `alternative`.
- A10: drivable `direct` khoét quanh xe phía trước và lấn sang làn bên phải. Làn xe đạp được gán `alternative`. `weather` nên là `rain`.
- A12 biển ONE WAY ghi `information`; đúng là `mandatory`. Đèn người đi bộ chưa gán.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
