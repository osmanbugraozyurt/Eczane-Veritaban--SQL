# Eczane Veritaban SQL

## VERİTABANI DİYAGRAMI

![Diagram](https://user-images.githubusercontent.com/116449607/199587416-aff0c96c-5edc-4db0-a6e6-95babbd79c89.png)

## SORGULAR

1) **_İl Bilgileri_**
```ruby
Create Table Iller (PlakaKod int IDENTITY(1,1) Primary Key, Il varchar(100))
```

2) **_İlçe Bilgileri_**
```ruby
Create Table Ilceler (ID int IDENTITY(1,1) Primary Key, Ilce varchar(100),
	PlakaKod int Foreign Key (PlakaKod) References Iller(PlakaKod))
```

3) **_Eczane Bilgileri_**
```ruby
Create Table EczaneBilgi (ID int IDENTITY(1,1) Primary Key, Ad varchar(100),
	IlcePostaKodu int Foreign Key (IlcePostaKodu) References Ilceler(ID),
Adres varchar(200))
```

4) **_Eczane Personel Bilgileri_**
```ruby
Create Table EczanePersonel (ID int IDENTITY(1,1) Primary Key, Ad varchar(100),
Soyad varchar(100), Unvan varchar(100), CepNumarası char(11), IseGirisTarihi smalldatetime, Maas money,
	EczaneBilgisi int Foreign Key (EczaneBilgisi) References EczaneBilgi(ID))
```

5) **_İlaç ile İlgili Tüm Bilgiler_**
```ruby
Create Table Ilaclar (ID int IDENTITY(1,1) Primary Key, Barkod varchar(100), IlacAdı varchar(100), EtkinMadde varchar(100),
ATCKodu varchar(100), RuhsatSahibi varchar(100), RuhsatTarihi smalldatetime, RuhsatNumarası varchar(100), KullanımYasi varchar(5),
Fiyat float)
```

6) **_Tedarikçi Bilgileri_**
```ruby
Create Table Tedarikci (ID int IDENTITY(1,1) Primary Key, FirmaAdı varchar(100),
	IlceBilgisi int Foreign Key  (IlceBilgisi) References Ilceler(ID),
Adres varchar(200))
```

7) **_İlaç Stok Bilgileri_**
```ruby
Create Table IlacStokBilgisi (ID int IDENTITY(1,1) Primary Key, UretimTarihi smalldatetime, SonTuketimTarihi smalldatetime,
AlimTarihi smalldatetime, 
	TedarikciBilgisi int Foreign Key (TedarikciBilgisi) References Tedarikci(ID),
	EczaneID int Foreign Key (EczaneID) References EczaneBilgi(ID),
	IlacAdet int)
```

8) **_Sigorta Bilgisi_**
```ruby
Create Table SigortaBilgisi (ID int IDENTITY(1,1) Primary Key, 
Ad varchar(100), İndirimOranı varchar(50))
```

9) **_Hasta Bilgileri_**
```ruby
Create Table HastaBilgisi (ID int IDENTITY(1,1) Primary Key, Ad varchar(100), Soyad varchar(100),
	IlceID int Foreign Key (IlceID) References Ilceler(ID),
	SigortaID int Foreign Key (SigortaID) References SigortaBilgisi(ID))
```

10) **_Satılan İlaç Bilgileri_**
```ruby
Create Table SatilanIlaclar (IlacID int Foreign Key (IlacID) References Ilaclar(ID),
SatisTarihi smalldatetime, KutuAdedi int, SatisSekli varchar(100),
	SatanPersonelID int Foreign Key (SatanPersonelID) References EczanePersonel(ID))
```

11) **_İade Edilen İlaç Bilgileri_**
```ruby
Create Table IadeEdilenIlaclar (IlacID int Foreign Key (IlacID) References Ilaclar(ID),
SatisTarihi smalldatetime, IadeTarihi smalldatetime,
	SatanPersonelID int Foreign Key (SatanPersonelID) References EczanePersonel(ID),
	IadeAlanPersonelID int Foreign Key (IadeAlanPersonelID) References EczanePersonel(ID),
	EczaneID int Foreign Key (EczaneID) References EczaneBilgi(ID))
```
