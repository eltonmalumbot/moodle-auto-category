import os
import requests

# ==============================================================================
# SENSOR KEAMANAN (Membaca kredensial dari Environment Variables sistem)
# Nilai di bawah ini sengaja menggunakan placeholder agar aman di GitHub.
# ==============================================================================
MOODLE_URL = os.environ.get("MOODLE_SERVER_URL", "https://link-moodle-anda-disini.sch.id") 
TOKEN = os.environ.get("MOODLE_API_TOKEN", "RAHASIA_TOKEN_API_ANDA") 

# Daftar lengkap 8 sekolah beserta ID kategori aslinya yang sudah Anda kumpulkan
DAFTAR_SEKOLAH = [
    {"nama_sekolah": "SMPK 1", "parent_id": 69},
    {"nama_sekolah": "SMPK 2", "parent_id": 70}
]

def call_moodle_api(function_name, params):
    # Validasi awal untuk mencegah eksekusi jika token belum dikonfigurasi di terminal lokal
    if TOKEN in ["RAHASIA_TOKEN_API_ANDA", ""]:
        return {"error": "Token API Moodle belum diatur di terminal atau masih tersensor!"}
        
    url = f"{MOODLE_URL.rstrip('/')}/webservice/rest/server.php"
    params.update({'wstoken': TOKEN, 'wsfunction': function_name, 'moodlewsrestformat': 'json'})
    try:
        return requests.post(url, data=params).json()
    except Exception as e:
        return {"error": str(e)}

def create_category(name, parent_id):
    params = {
        'categories[0][name]': name, 
        'categories[0][parent]': parent_id, 
        'categories[0][descriptionformat]': 1
    }
    return call_moodle_api('core_course_create_categories', params)

def main():
    print("--- MEMULAI PROSES PEMBUATAN KATEGORI MASSAL UNTUK SEMUA SMPK ---")
    
    for sekolah in DAFTAR_SEKOLAH:
        nama = sekolah["nama_sekolah"]
        pid = sekolah["parent_id"]
        
        print(f"\n[PROSES] Membuat kategori untuk {nama} di Parent ID: {pid}...")
        
        # 1. Membuat Kategori Tahun Ajaran Utama di dalam sekolah tersebut
        parent_res = create_category(f"{nama} Tahun Ajaran 2627", parent_id=pid)
        
        if isinstance(parent_res, list) and len(parent_res) > 0:
            new_parent_id = parent_res[0]['id']
            print(f"   => [SUKSES] Terbuat folder TA: '{nama} Tahun Ajaran 2627' (ID: {new_parent_id})")
            
            # 2. Daftar sub-kategori Kelas SMP (7, 8, 9) & Ujian yang otomatis masuk ke dalamnya
            sub_categories = [
                f"{nama} - Kelas 7", 
                f"{nama} - Kelas 8", 
                f"{nama} - Kelas 9", 
                f"PTS {nama} Semester 1 2627", 
                f"PTS {nama} Semester 2 2627", 
                f"PAS {nama} 2627", 
                f"PAT {nama} 2627", 
                f"US {nama} 2627"
            ]
            
            for sub_name in sub_categories:
                sub_res = create_category(sub_name, parent_id=new_parent_id)
                if isinstance(sub_res, list) and len(sub_res) > 0:
                    print(f"       > Terbuat: '{sub_name}' (ID: {sub_res[0]['id']})")
                else:
                    print(f"       [GAGAL] Gagal membuat sub-kategori: {sub_name}")
        else:
            print(f"   => [GAGAL] Gagal mengeksekusi {nama}. Respon: {parent_res}")

    print("\n==================================================================")
    print(" PROSES MASSAL SELESAI! Silakan cek kembali halaman Moodle Anda. ")
    print("==================================================================")

if __name__ == "__main__":
    main()
