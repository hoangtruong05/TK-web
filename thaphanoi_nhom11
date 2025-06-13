import heapq

def h_n(coc, so_dia):
    """
    Hàm heuristic: đếm số đĩa chưa đúng vị trí trên cọc C (cọc đích).
    """
    so_dia_sai = 0
    for i in range(so_dia):
        if len(coc[2]) > i and coc[2][i] == so_dia - i:
            continue
        so_dia_sai += 1
    return so_dia_sai

def gia_tri_f(so_buoc, coc, so_dia):
    """
    Tính giá trị hàm f = g + h cho thuật toán AKT
    """
    return so_buoc + h_n(coc, so_dia)

def tao_nuoc_di(coc):
    """
    Tạo danh sách các nước đi hợp lệ (theo luật tháp Hà Nội).
    """
    nuoc_di = []
    for coc_nguon in range(3):
        if not coc[coc_nguon]:
            continue
        for coc_dich in range(3):
            if coc_nguon != coc_dich and (not coc[coc_dich] or coc[coc_dich][-1] > coc[coc_nguon][-1]):
                nuoc_di.append((coc_nguon, coc_dich))
    return nuoc_di

def ap_dung_nuoc_di(coc, nuoc_di):
    """
    Áp dụng một nước đi để tạo trạng thái mới.
    """
    coc_nguon, coc_dich = nuoc_di
    coc_moi = [c[:] for c in coc]  # sao chép từng cọc
    coc_moi[coc_dich].append(coc_moi[coc_nguon].pop())
    return coc_moi

def kiem_tra_dich(coc, so_dia):
    """
    Kiểm tra nếu tất cả các đĩa đã ở cọc C theo đúng thứ tự.
    """
    return coc[2] == list(range(so_dia, 0, -1))

def thap_Ha_Noi_AKT(so_dia):
    """
    Thuật toán AKT để giải bài toán tháp Hà Nội.
    """
    coc_ban_dau = [[i for i in range(so_dia, 0, -1)], [], []]
    MO = [(gia_tri_f(0, coc_ban_dau, so_dia), 0, coc_ban_dau, [])]
    DONG = set()

    while MO:
        _, so_buoc, coc, cac_buoc = heapq.heappop(MO)
        trang_thai_coc = tuple(tuple(c) for c in coc)
        if trang_thai_coc in DONG:
            continue

        DONG.add(trang_thai_coc)

        if kiem_tra_dich(coc, so_dia):
            print(f'\nĐã tìm thấy lời giải sau {len(cac_buoc)} bước:')
            for buoc in cac_buoc:
                print(buoc)
            return

        for nuoc_di in tao_nuoc_di(coc):
            coc_moi = ap_dung_nuoc_di(coc, nuoc_di)
            coc_nguon = nuoc_di[0]
            dia_di_chuyen = coc[coc_nguon][-1]  # lấy đĩa trước khi di chuyển
            buoc_moi = cac_buoc + [f"Di chuyển đĩa {dia_di_chuyen} từ {chr(65 + coc_nguon)} đến {chr(65 + nuoc_di[1])}"]
            heapq.heappush(MO, (gia_tri_f(so_buoc + 1, coc_moi, so_dia), so_buoc + 1, coc_moi, buoc_moi))

    print(" Không tìm được lời giải.")

if __name__ == '__main__':
    try:
        so_dia = int(input('Nhập số đĩa: '))
        if so_dia <= 0:
            print("Số đĩa phải lớn hơn 0.")
        else:
            thap_Ha_Noi_AKT(so_dia)
    except ValueError:
        print("Vui lòng nhập một số nguyên.")
        so_dia = int(input('Nhập số đĩa: '))
        thap_Ha_Noi_AKT(so_dia)
