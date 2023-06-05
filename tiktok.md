den = "\033[1;90m"
luc = "\033[1;32m"
trang = "\033[1;37m"
red = "\033[1;31m"
vang = "\033[1;33m"
tim = "\033[1;35m"
lamd = "\033[1;34m"
lam = "\033[1;36m"
purple = "\e[35m"
hong = "\033[1;95m"
os.system('title TOOL TRAO DOI SUB TIKTOK')
thanh_xau= trang + "~" + red + "[" + vang+ "⟨⟩" + red + "] " + trang + "➩ "
thanh_dep= trang + "~" + red + "[" + luc + "✓" + red + "] " + trang + "➩ "
##### Cài Thư Viện #####
from pystyle import Add, Center, Anime, Colors, Colorate, Write, System
import requests, json
import os
from sys import platform
from time import sleep
from datetime import datetime
from time import strftime
total = 0
may = 'mb' if platform[0:3] == 'lin' else 'pc'
def banner():
	pass
def now(so):
	for i in range(so):
		print(red+'────', end = '' )
	print('')
class TraoDoiSub_Api (object):
	def __init__ (self, token):
		self.token = token
	
	def main(self):
		try:
			main = requests.get('https://traodoisub.com/api/?fields=profile&access_token='+self.token).json()
			try:
				return main['data']
			except:
				False
		except:
			return False
	def run(self, user):
		try:
			run = requests.get(f'https://traodoisub.com/api/?fields=tiktok_run&id={user}&access_token={self.token}').json()
			try:
				return run['data']
			except:
				return False
		except:
			return False
	#tiktok_like, tiktok_follow
	def get_job(self, type):
		try:
			get = requests.get(f'https://traodoisub.com/api/?fields={type}&access_token={self.token}')
			return get
		except:
			return False
	
	def cache(self, id, type):
#TIKTOK_LIKE_CACHE, TIKTOK_FOLLOW_CACHE
		try:
			cache = requests.get(f'https://traodoisub.com/api/coin/?type={type}&id={id}&access_token={self.token}').json()
			try:
				cache['cache']
				return True
			except:
				return False
		except:
			return False

	def nhan_xu(self, id, type):
		try:
			nhan = requests.get(f'https://traodoisub.com/api/coin/?type={type}&id={id}&access_token={self.token}')
			try:
				xu = nhan.json()['data']['xu']
				msg = nhan.json()['data']['msg']
				job = nhan.json()['data']['job_success']
				xuthem = nhan.json()['data']['xu_them']
				global total
				total+=xuthem
				now(14)
				print(f'{lam}Nhận Thành Công {job} Nhiệm Vụ {red}| {luc}{msg} {red}| {luc}TOTAL {vang}{total} {luc}Xu {red}| {vang}{xu} ')
				now(14)
				if job == 0:
					return 0
			except:
				if '"code":"error","msg"' in nhan.text:
					hien = nhan.json()['msg']; print(red+hien, end = '\r'); sleep(2); print(' '*len(hien), end = '\r')
				else:
					print(red+'Nhận Xu Thất Bại !', end = '\r'); sleep(2); print('                                                       ', end = '\r')
				return False
		except:
			print(red+'Nhận Xu Thất Bại !', end = '\r'); sleep(2); print('                                                       ', end = '\r')
			return False
def delay(dl):
  try:
    for i in range(dl, -1, -1):
       print(f'{vang}[{trang}FRIVE-TOOL{vang}][{trang}'+str(i)+vang+']           ',end='\r')
       sleep(1)
  except:
     sleep(dl)
     print(dl,end='\r')

def chuyen(link, may):
	if may == 'mb':
		os.system(f'xdg-open {link}')
	else:
		os.system(f'cmd /c start {link}')




#----------------------------------------------------------------------------



def main():
	dem=0
	banner()
	while True:
		if os.path.exists('configtds.txt'):
			with open('configtds.txt', 'r') as f:
				token = f.read()
			tds = TraoDoiSub_Api(token)
			data = tds.main()
			try:
				print(f'{thanh_xau}{luc}Nhập {vang}[{trang}1{vang}] {luc}Giữ Lại Tài Khoản '+vang+ data['user'] )
				print(f'{thanh_xau}{luc}Nhập {vang}[{trang}2{vang}] {luc}Nhập Access_Token TDS Mới')
				chon = input(f'{thanh_xau}{luc}Nhập {trang}===>: {vang}')
				if chon == '2':
					os.remove('configtds.txt')
				elif chon == '1':
					pass
				else:
					print(red+'Lựa chọn không xác định !!!');now(14)
					continue 
			except:
				os.remove('configtds.txt')
		if not os.path.exists('configtds.txt'):
			token = input(f'{thanh_xau}{luc}Nhập Access_Token TDS: {vang}')
			with open('configtds.txt', 'w') as f:
				f.write(token)
		with open('configtds.txt', 'r') as f:
			token = f.read()
		tds = TraoDoiSub_Api(token)
		data = tds.main()
		try:
			xu = data['xu']
			xudie = data['xudie']
			user = data['user']
			print(lam+' Đăng Nhập Thành Công ')
			break
		except:
			print(red+'Access Token Không Hợp Lệ! Xin Thử Lại ')
			os.remove('configtds.txt')
			continue 
	now(14)
	
		
	banner()
	print(f'{thanh_xau}{luc}Tên Tài Khoản: {vang}{user} ')
	print(f'{thanh_xau}{luc}Xu Hiện Tại: {vang}{xu}')
	print(f'{thanh_xau}{luc}Xu Bị Phạt: {vang}{xudie} ')
	while True:
		ntool=0
		now(14)
		print(f'{thanh_xau}{luc}Nhập {red}[{vang}1{red}] {luc}Để Chạy Nhiệm Vụ Tim')
		print(f'{thanh_xau}{luc}Nhập {red}[{vang}2{red}] {luc}Để Chạy Nhiệm Vụ Follow')
		print(f'{thanh_xau}{luc}Nhập {red}[{vang}3{red}] {luc}Để Chạy Nhiệm Vụ Follow Tiktok Now')
		nhiem_vu=input(f'{thanh_xau}{luc}Nhập Số Để Chạy Nhiệm Vụ: {vang}')
		dl = int(input(f'{thanh_xau}{luc}Nhập Delay: {vang}'))
		while True:
			if ntool == 2:
				break
			ntool = 0
			now(14)
			nv_nhan=int(input(f'{thanh_xau}{luc}Sau Bao Nhiêu Nhiệm Vụ Thì Nhận Xu: {vang}'))
			if nv_nhan < 8:
				print(red+'Trên 8 Nhiệm Vụ Mới Được Nhận Tiền!')
				continue
			if nv_nhan > 15:
				print(red+'Nhận Xu Dưới 15 Nhiệm Vụ Để Tránh Lỗi')
				continue
			user_cau_hinh=input(f'{thanh_xau}{luc}Nhập User Name Tik Tok Cần Cấu Hình: {vang}')
			cau_hinh=tds.run(user_cau_hinh)
			if cau_hinh != False:
				user=cau_hinh['uniqueID']
				id_acc=cau_hinh['id']
				now(14)
				print(f'{luc}Đang Cấu Hình ID: {vang}{id_acc} {red}| {luc}User: {vang}{user} {red}| ')
				now(14)
			else:
				print(f'{red}Cấu Hinh Thất Bại User: {vang}{user_cau_hinh} ')
				continue 
			while True:
				if ntool==1 or ntool==2:break
				if '1' in nhiem_vu:
					listlike = tds.get_job('tiktok_like')
					if listlike == False:
						print(red+'Không Get Được Nhiệm Vụ Like              ', end = '\r');sleep(2); print('                                                        ', end = '\r')
					elif 'error' in listlike.text:
						if listlike.json()['error'] == 'Thao tác quá nhanh vui lòng chậm lại':
							coun = listlike.json()['countdown']
							print(f'{red}Đang Get Nhiệm Vụ Like, COUNTDOWN: {str(round(coun, 3))} ', end = '\r'); sleep(2); print('                                                       ', end = '\r')
						elif listlike.json()['error'] == 'Vui lòng ấn NHẬN TẤT CẢ rồi sau đó tiếp tục làm nhiệm vụ để tránh lỗi!':
							nhan = tds.nhan_xu('TIKTOK_LIKE_API', 'TIKTOK_LIKE') #TIKTOK_LIKE, TIKTOK_FOLLOW, TIKTOK_COMMENT
						else:
							print(red+listlike.json()['error'] , end ='\r');sleep(2); print('                                                        ', end = '\r')
					else:
						try:
							listlike = listlike.json()['data']
						except:
							print(red+'Hết Nhiệm Vụ Like                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							continue
						if len(listlike) == 0:
							print(red+'Hết Nhiệm Vụ Like                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
						else:
							print(f'{luc}Tìm Thấy {vang}{len(listlike)} {luc}Nhiệm Vụ Like                       ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							for i in listlike:
								id = i['id']
								link = i['link']
								chuyen(link, may)
								cache = tds.cache(id, 'TIKTOK_LIKE_CACHE')
								if cache != True:
									tg=datetime.now().strftime('%H:%M:%S')
									hien = f'{vang}[{red}X{vang}] {red}| {lam}{tg} {red}| {vang}TIM {red}| {trang}{id} {red}|'; print(hien, end = '\r');sleep(1); print('                                                                                        ', end = '\r')
								else:
									dem+=1
									tg=datetime.now().strftime('%H:%M:%S')
									print(f'{vang}[{trang}{dem}{vang}] {red}| {lam}{tg} {red}| {Colorate.Horizontal(Colors.yellow_to_red, "TIM")} {red}| {trang}{id} {red}|')
									delay(dl)
									if dem % nv_nhan == 0:
										nhan = tds.nhan_xu('TIKTOK_LIKE_API', 'TIKTOK_LIKE')
										if nhan == 0:
											print(luc+'Nhận Xu Thất Bại Acc Tiktok Của Bạn Ổn Chứ ') 
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}1{red}] {luc}Để Thay Nhiệm Vụ ')
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}2{red}] {luc}Thay Acc Tiktok ')
											print(f'{thanh_xau}{luc}Nhấn {red}[{vang}Enter{red}] {luc}Để Tiếp Tục')
											chon=input(f'{thanh_xau}{luc}Nhập {trang}===>: {vang}')
											if chon == '1':
												ntool=2
												break
											elif chon =='2':
												ntool = 1
												break
											now(14)
				if ntool==1 or ntool==2:break
				if '2' in nhiem_vu:
					listfollow = tds.get_job('tiktok_follow')
					if listfollow == False:
						print(red+'Không Get Được Nhiệm Vụ Follow              ', end = '\r');sleep(2); print('                                                        ', end = '\r')
					elif 'error' in listfollow.text:
						if listfollow.json()['error'] == 'Thao tác quá nhanh vui lòng chậm lại':
							coun = listfollow.json()['countdown']
							print(red+f'Đang Get Nhiệm Vụ Follow, COUNTDOWN: {str(round(coun, 3))} ', end = '\r'); sleep(2); print('                                                       ', end = '\r')
						elif listfollow.json()['error'] == 'Vui lòng ấn NHẬN TẤT CẢ rồi sau đó tiếp tục làm nhiệm vụ để tránh lỗi!':
							nhan = tds.nhan_xu('TIKTOK_FOLLOW_API', 'TIKTOK_FOLLOW') #TIKTOK_LIKE, TIKTOK_FOLLOW, TIKTOK_COMMENT
						else:
							print(red+listfollow.json()['error'] , end ='\r');sleep(2); print('                                                        ', end = '\r')
					else:
						try:
							listfollow = listfollow.json()['data']
						except:
							print(red+'Hết Nhiệm Vụ Follow                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							continue
						if len(listfollow) == 0:
							print(red+'Hết Nhiệm Vụ Follow                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
						else:
							print(luc+f'Tìm Thấy {vang}{len(listfollow)} {luc}Nhiệm Vụ Follow                       ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							for i in listfollow:
								id = i['id']
								link = i['link']
								chuyen(link, may)
								cache = tds.cache(id, 'TIKTOK_FOLLOW_CACHE')
								if cache != True:
									tg=datetime.now().strftime('%H:%M:%S')
									hien = f'{vang}[{red}X{vang}] {red}| {lam}{tg} {red}| {vang}FOLLOW {red}| {trang}{id} {red}|'; print(hien, end = '\r');sleep(1); print('                                                                                        ', end = '\r')
								else:
									dem+=1
									tg=datetime.now().strftime('%H:%M:%S')
									print(f'{vang}[{trang}{dem}{vang}] {red}| {lam}{tg} {red}| {Colorate.Horizontal(Colors.yellow_to_red, "FOLLOW")} {red}| {trang}{id} {red}|')
									delay(dl)
									if dem % nv_nhan == 0:
										nhan = tds.nhan_xu('TIKTOK_FOLLOW_API', 'TIKTOK_FOLLOW')
										if nhan == 0:
											print(luc+'Nhận Xu Thất Bại Acc Tiktok Của Bạn Ổn Chứ ') 
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}1{red}] {luc}Để Thay Nhiệm Vụ ')
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}2{red}] {luc}Thay Acc Tiktok ')
											print(f'{thanh_xau}{luc}Nhấn {red}[{vang}Enter{red}] {luc}Để Tiếp Tục')
											chon=input(f'{thanh_xau}{luc}Nhập {trang}===>: {vang}')
											if chon == '1':
												ntool=2
												break
											elif chon =='2':
												ntool = 1
												break
											now(14)
				if ntool==1 or ntool==2:break
				if '3' in nhiem_vu:
					listfollow = tds.get_job('tiktok_follow')
					if listfollow == False:
						print(red+'Không Get Được Nhiệm Vụ Follow              ', end = '\r');sleep(2); print('                                                        ', end = '\r')
					elif 'error' in listfollow.text:
						if listfollow.json()['error'] == 'Thao tác quá nhanh vui lòng chậm lại':
							coun = listfollow.json()['countdown']
							print(f'{red}Đang Get Nhiệm Vụ Follow, COUNTDOWN: {str(round(coun, 3))} ', end = '\r'); sleep(2); print('                                                       ', end = '\r')
						elif listfollow.json()['error'] == 'Vui lòng ấn NHẬN TẤT CẢ rồi sau đó tiếp tục làm nhiệm vụ để tránh lỗi!':
							nhan = tds.nhan_xu('TIKTOK_FOLLOW_API', 'TIKTOK_FOLLOW') #TIKTOK_LIKE, TIKTOK_FOLLOW, TIKTOK_COMMENT
						else:
							print(red+listfollow.json()['error'] , end ='\r');sleep(2); print('                                                        ', end = '\r')
					else:
						try:
							listfollow = listfollow.json()['data']
						except:
							print(red+'Hết Nhiệm Vụ Follow                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							continue
						if len(listfollow) == 0:
							print(red+'Hết Nhiệm Vụ Follow                             ', end = '\r');sleep(2); print('                                                        ', end = '\r')
						else:
							print(f'{luc}Tìm Thấy {vang}{len(listfollow)} {luc}Nhiệm Vụ Follow                       ', end = '\r');sleep(2); print('                                                        ', end = '\r')
							for i in listfollow:
								id = i['id']
								uid = id.split('_')[0] 
								link = i['link']
								que = i['uniqueID']
								if may == 'mb':
									chuyen(f'tiktoknow://user/profile?user_id={uid}', may)
								else:
									chuyen(f'https://now.tiktok.com/@{que}', may)
								cache = tds.cache(id, 'TIKTOK_FOLLOW_CACHE')
								if cache != True:
									tg=datetime.now().strftime('%H:%M:%S')
									hien = f'{vang}[{red}X{vang}] {red}| {lam}{tg} {red}| {vang}FOLLOW_TIKTOK_NOW {red}| {trang}{id} {red}|'; print(hien, end = '\r');sleep(1); print('                                                                                        ', end = '\r')
								else:
									dem+=1
									tg=datetime.now().strftime('%H:%M:%S')
									print(f'{vang}[{trang}{dem}{vang}] {red}| {lam}{tg} {red}| {Colorate.Horizontal(Colors.yellow_to_red, "FOLLOW_TIKTOK_NOW")} {red}| {trang}{id} {red}|')
									delay(dl)
									if dem % nv_nhan == 0:
										nhan = tds.nhan_xu('TIKTOK_FOLLOW_API', 'TIKTOK_FOLLOW')
										if nhan == 0:
											print(luc+'Nhận Xu Thất Bại Acc Tiktok Của Bạn Ổn Chứ ') 
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}1{red}] {luc}Để Thay Nhiệm Vụ ')
											print(f'{thanh_xau}{luc}Nhập {red}[{vang}2{red}] {luc}Thay Acc Tiktok ')
											print(f'{thanh_xau}{luc}Nhấn {red}[{vang}Enter{red}] {luc}Để Tiếp Tục')
											chon=input(f'{thanh_xau}{luc}Nhập {trang}===>: {vang}')
											if chon == '1':
												ntool=2
												break
											elif chon =='2':
												ntool = 1
												break
											now(14)
main()
