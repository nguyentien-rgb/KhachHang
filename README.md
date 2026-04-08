using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace thuongxuyen1_KhachHang
{
    internal class KhachHang
    {
        private string _MaKhachHang;
        public string MaKhachHang
        {
            get { return _MaKhachHang; }
            set { _MaKhachHang = value; }
        }
        private string _GioiTinh;
        public string GioiTinh
        {
            get { return _GioiTinh; }
            set { _GioiTinh = value; }
        }
        private double _SoLuongMua;
        public double SoLuongMua
        {
            get { return _SoLuongMua; }
            set { _SoLuongMua = value; }
        }
        private double _DonGia;
        public double DonGia
        {
            get { return _DonGia; }
            set { _DonGia = value; }
        }
        public KhachHang() { }
        public KhachHang(string MaKhachHang, string GioiTinh, double SoLuongMua, double DonGia)
        {
            this.MaKhachHang = MaKhachHang;
            this.GioiTinh= GioiTinh;    
            this.SoLuongMua= SoLuongMua;
            this.DonGia= DonGia;
        }
        public virtual double TongTien()
        {
            return SoLuongMua*DonGia;
        }
        public override bool Equals(object obj)
        {
            KhachHang KH = obj as KhachHang;
            return (this.MaKhachHang.Equals(KH.MaKhachHang));
        }
        public override string ToString()
        {
            return string.Format("{0, -15}{1, -15}{2, -15}{3, -15}{4, -15}", MaKhachHang, GioiTinh, SoLuongMua, DonGia, TongTien());
        }

    }
}
....
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace thuongxuyen1_KhachHang
{
    internal class KhachHangVip : KhachHang
    {
        private string _NgayLamThe;
        public string NgayLamThe
        {
            get { return _NgayLamThe; }
            set { _NgayLamThe = value; }
        }
        public KhachHangVip()
        {

        }
        public KhachHangVip(string MaKhachHang, string GioiTinh, double SoLuongMua, double DonGia, string NgayLamThe) : base(MaKhachHang, GioiTinh, SoLuongMua, DonGia)
        {
            this.NgayLamThe = NgayLamThe;
        }
        public override double TongTien()
        {
            double Tong = base.TongTien();
            if (Tong <= 1000)
                return Tong * 0.9;
            else
                return Tong * 0.8;
        }
        public override string ToString()
        {
            double TongTruocGiam = base.SoLuongMua * base.DonGia;
            string GiamGia = TongTruocGiam <= 1000 ? "10%" : "20%";
            return string.Format("{0, -15}{1, -15}{2,-15}{3,-15}{4,-15}{5,-15}{6,-15}", MaKhachHang, GioiTinh, NgayLamThe, SoLuongMua, DonGia, GiamGia, TongTien());
        }
    }
}
...
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace thuongxuyen1_KhachHang
{
    internal class Program
    {
        static List<KhachHang> DanhSach = new List<KhachHang>();
        static void Main(string[] args)
        {
            bool exit = false;
            do
            {
                Console.WriteLine("Menu cua chuong trinh: ");
                Console.WriteLine("1. Nhap thong tin");
                Console.WriteLine("2. Hien thi danh sach");
                Console.WriteLine("3. Xoa khach hang");
                Console.WriteLine("4. Thoat");
                Console.Write("Nhap lua chon: ");
                string LuaChon = Console.ReadLine();
                switch (LuaChon)
                {
                    case "1":
                        NhapThongTin();
                        break;
                    case "2":
                        HienThiDanhSach();
                        break;
                    case "3":
                        XoaKhachHang();
                        break;
                    case "4":
                        exit = true;
                        break;
                    default:
                        Console.WriteLine("nhap loi, vui long nhap lai!");
                        break;
                }

            }
            while (!exit);
        }
        private static void NhapThongTin()
        {
            Console.Write("1. Khach hang. | ");
            Console.WriteLine("2. Khach hang vip.");
            Console.Write("nhap lua chon cua ban: ");
            string LuaChon = Console.ReadLine();
            switch (LuaChon)
            {
                case "1":
                    KhachHang KH = new KhachHang();
                    Console.WriteLine("Nhap ma khach hang: ");
                    KH.MaKhachHang = Console.ReadLine();
                    if (DanhSach.Contains(KH))
                    {
                        Console.WriteLine("Da co khach hang trong danh sach");
                        Console.ReadLine();
                    }
                    else
                    {
                        Console.WriteLine("Nhap gioi tinh: ");
                        KH.GioiTinh = Console.ReadLine();
                        Console.WriteLine("nhap so luong mua: ");
                        KH.SoLuongMua = double.Parse(Console.ReadLine());
                        Console.WriteLine("Nhap don gia: ");
                        KH.DonGia = double.Parse(Console.ReadLine());
                        DanhSach.Add(KH);

                    }
                    break;
                case "2":
                    KhachHangVip KHV = new KhachHangVip();
                    Console.WriteLine("Nhap ma khach hang vip: ");
                    KHV.MaKhachHang = Console.ReadLine();
                    if (DanhSach.Contains(KHV))
                    {
                        Console.WriteLine("Da co khach hang trong danh sach");
                        Console.ReadLine();
                    }
                    else
                    {
                        Console.WriteLine("nhap gioi tinh: ");
                        KHV.GioiTinh = Console.ReadLine();
                        Console.WriteLine("nhap ngay lam the (ngay-thang-nam): ");
                        KHV.NgayLamThe = Console.ReadLine();
                        Console.WriteLine("nhap so luong mua: ");
                        KHV.SoLuongMua = double.Parse(Console.ReadLine());
                        Console.WriteLine("nhap don gia: ");
                        KHV.DonGia = double.Parse(Console.ReadLine());
                        DanhSach.Add(KHV);
                    }
                    break;
                default:
                    Console.WriteLine("ko hop le!");
                    break;

            }
        }
        private static void HienThiDanhSach()
        {
            Console.WriteLine("{0, -15}{1, -15}{2,-15}{3,-15}{4,-15}{5,-15}{6,-15}", "Ma", "Gioi tinh", "Ngay lam the", "So luong", "Don gia", "Giam gia", "Tong tien");
            foreach (KhachHang So in DanhSach)
            {
                Console.WriteLine(So.ToString());
            }
        }
        private static void XoaKhachHang()
        {
            Console.Write("Nhap ma khach hang can xoa: ");
            string Ma = Console.ReadLine();
            KhachHang KHTam = new KhachHang();
            KHTam.MaKhachHang = Ma;

            if (DanhSach.Contains(KHTam))
            {
                DanhSach.Remove(KHTam);
                Console.WriteLine("Da xoa khach hang. Danh sach sau khi xoa:");
                HienThiDanhSach();
            }
            else
            {
                Console.WriteLine("Khong tim thay khach hang de xoa.");
            }
        }
    }
}

