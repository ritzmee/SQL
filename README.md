# SQL
use MRP
create table customer
( customer_id varchar(30) PRIMARY KEY,
  customer_name varchar(50),
  active_status char(10),
  customer_email varchar(100),
  customer_birthdate date,
  customer_phone varchar(12),
  gender char(10),
);
--T2
create table supplier
( 
  supplier_id varchar(30) PRIMARY KEY,
  supplier_name varchar(50),
  active_status char(10),
  supplier_email varchar(100),
  supplier_phone varchar(12)
 
);
--T3
create table log_in_id
(
login_id varchar(30) primary key,
username varchar(30)
);
--T4
create table log_in
( 
  username varchar(50) primary key,
  pass_word varchar(20),
  shortcode char(1),
  );
--T5
create table user_type
( 
  type_of_user varchar(50),
  shortcode char(1) primary key
);
--T9
create table Country(
  Country_id varchar(30) primary key,
  country_name    varchar(30) 
  );
--T10
create table states(
   State_id varchar(30) primary key,
   state_name varchar(30),
   fk_country_id varchar(30),
   foreign key (fk_country_id) references country(country_id)
);
--T11
create table district
( 
  District_id varchar(30) primary key,
  distict_name varchar(30),
  fk_state_id varchar(30)
   foreign key (fk_state_id) references states(state_id)
);

--T12
create table Area
( 
  postal_code varchar(30) primary key,
  Area varchar(30),
  fk_district_id varchar(30),
  foreign key (fk_district_id) references district(District_id)
);
--T6
create table Customer_Address
( 
  Cutomer_Add_Id varchar(30) primary key,
  fk_Customer_ID varchar(30),
  Flat_no varchar(30),
  Society varchar(30),
  fk_postal_code varchar(30),
  foreign key(fk_Customer_ID) references customer(customer_id),
  foreign key(fk_postal_code) references area(postal_code)
  );
--T7
create table Supplier_Address(
 
  Supplier_Add_ID varchar(30) primary key,
  fk_supplier_id varchar(30),
  Flat_no varchar(30),
  Society varchar(30),
  fk_postal_code varchar(30),
  foreign key(fk_supplier_id) references supplier(supplier_id),
  foreign key(fk_postal_code) references area(postal_code)
);
--T8
create table login_details(
  shopping_session varchar(30) primary key,
  username varchar(30),
  login_time datetime,
  logout_time datetime
);


---------------Product-----------------------
--T13
create table Category(
    Category_ID    varchar(30) Primary key,
    Category_Name varchar(30)
);
--T14
create table Sub_category(
    Sub_Category_ID    varchar(30) Primary key,
    Sub_Category_Name varchar(30),
	fk_Category_ID varchar(30),
	foreign key(fk_Category_ID) references Category(Category_ID)
);

--T15
create table Product_Info(
    Product_Id varchar(30) Primary key,
    Product_Name varchar(30),
    Size varchar(50),
    wght_kg float,
    sku int,
    cost float,
    Brand varchar(30),
    Origin varchar(30),
    LT int,
	fk_subcategory_id varchar(30),
	foreign key(fk_subcategory_id) references Sub_category(Sub_Category_ID)
);
--T16
create table Stock(
    ck_supplier_ID varchar(30) ,
    ck_product_Id varchar(30) ,
    Product_stock int,
	primary key(ck_supplier_ID, ck_product_Id)
);
--------------------------Order---------------------------------------------
--T17
create table Order_info(
    Order_id varchar(30) primary key, 
    fk_Customer_id varchar(30),
    Order_date date,
    Required_date date,
    Shipment_ID    varchar(30),
    Amount    float,
    payment_Date date,
    Transaction_status varchar(30),
	foreign key(fk_Customer_id) references customer(customer_id)
);
--T18
create table Product_order1(
    product_Order_ID varchar(30) primary key,
	fk_supplier_add_id varchar(30),
    fk_Product_Id varchar(30),
    Qty int,
    fk_Discount__coupon_id float,
    Total_price float,
	fk_order_id varchar(30),
	gift_msg varchar(200),
	foreign key(fk_supplier_add_id) references customer(customer_id),
	foreign key(fk_Product_Id) references Supplier_Address(Supplier_Add_ID),
	foreign key(fk_order_id) references order_info(order_id)
);
--T19
create table Payment_Type(
    Payment_type varchar(30),
    Payment_type_ID varchar(30) primary key
);
--T20
create table Payment(
    fk_Order_ID varchar(30),
    Payment_id varchar(30) Primary key,
    fk_Payment_Type_ID varchar(30),
    Time_Stamp datetime,
	foreign key(fk_Order_ID) references order_info(order_id),
	foreign key(fk_Payment_Type_ID) references Payment_Type(Payment_type_ID)
);
--T21

create table Suplier_PaymentType_details( 
   Pay_Id varchar(30) primary key,
   fk_Supplier_ID    varchar(30),
   fk_Payment_type_ID varchar(30),
	foreign key(fk_Payment_Type_ID) references Payment_Type(Payment_type_ID),
	foreign key(fk_Supplier_ID) references supplier(supplier_id)
);
--T22
create table Shipment(
    Shipment_ID varchar(30) Primary key,
    Ship_date date,
    Ship_method varchar(30),
    Expected_Delivery_Date date,
    Delivery_Status varchar(30),
	Order_received_Date date,
    Order_packed_Date date,
	);
-----------BANK DETAILS-----------------------
--T23
create table Customer_BankDetails(
fk_cutomer_id varchar(30),	
Account_no int primary key,	
bank_Name varchar(50),	
IFSC_code varchar(30),	
Account_holder_name varchar(100)
foreign key(fk_cutomer_id) references Customer(customer_id)
);
--T24
create table Supplier_BankDetails(
fk_supplier_id varchar(30),	
Account_no int primary key,	
bank_Name varchar(50),	
IFSC_code varchar(30),	
Account_holder_name varchar(100)
foreign key(fk_supplier_id) references Supplier(supplier_id)
);
--T25
create table Branch_Details(
Branch varchar(100),	
IFSC_code int primary key
);
---------------UPI Details ---------------------
--T26
create table UPI_Details(
UPI_ID varchar(50) primary key,	
fk_cutomer_id varchar(30),
foreign key(fk_cutomer_id) references Customer(customer_id)
);
--------------------Review-------------------------------
--T27
create table review(
   Review_id varchar(30) primary key,
   fk_Product_Id varchar(30),
   fk_Customer_ID varchar(30),
   Rating float,
   Review varchar(30),
   Review_Datetime datetime,
   foreign key(fk_Customer_ID) references Customer(customer_id),
   foreign key(fk_Product_Id) references product_info(product_id)
);
-------------------Announcement--------------------------
--T28
create table Announcement(
description_id varchar(30) primary key,
description varchar(100),
descriptions_detail varchar(100),
startdate date,
end_date date,	
fk_category_ID varchar(30),
foreign key(fk_category_ID) references category(category_id)
);
--------------------Like/Wishlist----------------------------
--T29
create table wishlist(
ck_product_id varchar(30),
product_name varchar(50),
Like_Date date,	
ck_customer_id varchar(30)
primary key(ck_product_id, ck_customer_id)
);
--------------------notification------------------------------------
--T30
Create table msg(
        Msg_ID varchar(30) primary key,
        Message_Name varchar(50),
        Message_desc varchar(50)
        );
--T31
Create table notifications(
		notification_id varchar(30) primary key,
        fk_customer_Id varchar(30),
        fk_Msg_ID varchar(30),
        fk_Order_ID varchar(30),
        Message_Rec_Date date,
        Message_Rec_Time time,
		foreign key (fk_Msg_ID) references msg(Msg_ID),
		foreign key (fk_customer_Id) references customer(customer_ID),
		foreign key (fk_Order_ID) references order_info(order_ID)

        );
--T32
Create table Helpline(
        Helpline_No INT,
        Country_Initial varchar(50) primary key
        );
-------------------cart--------------------------------------------
--T33
Create table cart_customer(
        Cart_ID varchar(30) primary key,
        fk_customer_Id varchar(30)
		foreign key(fk_customer_Id) references customer(customer_Id)
        );
--T34
Create table discount(
        Discount_coupon_id varchar(30) primary key,
        Discount float,
        Discount_desc varchar(50)
        );
--T35
create table cart(
        fk_ck_Cart_ID varchar(30) ,
        ck_Product_Id varchar(30),
        Qty INT,
        cost float,
        fk_Discount_coupon_id varchar(30),
        Total_price float,
		foreign key (fk_ck_Cart_ID) references cart_customer(Cart_ID),
		foreign key (fk_Discount_coupon_id) references cart_customer(Cart_ID),
		primary key(fk_ck_Cart_ID, ck_Product_Id)
        );
--T36
create table FAQ(
	FAQ_id varchar(30) primary key,
	Question varchar(30),
	Answer varchar(30)
);
--T37
create table admin_info(
  admin_id varchar(30) primary key,
  admin_name varchar(30),
  admin_password varchar(30)
);
--T38
create table shipper(
	shipper_name varchar(30),
	company_name varchar(30),
	shipper_helpline varchar(30) primary key
);
--T39
create table service_center(
     location_name varchar(30),
	 contact_no int primary key
);
--T40
create table clearance_warehouse(
	warehouse_id varchar(30) primary key,
	warehouse_name varchar(30),
	warehouse_location varchar(30)
);

----------------------------------------------inserting values--------------------------------------------------------------
--T1
--select * from customer
insert into customer values('C1','Ruby Patel','Y','Ruby@gmail.com',	'4-March-89',	'F',	9076573489)
insert into customer values('C2',	'Summer Hayward', 'Y','Summer@gmail.com','21-May-97',	'F',	9145673909)
insert into customer values('C3',	'Devin Huddleston',	'Y',	'Devin@gmail.com',	'2-November-96',	'M',	9987567122)

--T2
insert into supplier values('S1',	'Vaughn',	'Y',	'Vaughn@gmail',	9076573888)
insert into supplier values('S2',	'William',	'Y',	'William@gmail',	9145674308)
insert into supplier values('S3',	'David',	'Y',	'David@gmail',	9987567521)
--select * from supplier

--T3
--select * from log_in_id
insert into log_in_id values('C1',	'ruby1')
insert into log_in_id values('C2',	'summer2')
insert into log_in_id values('C3','devin3')
insert into log_in_id values('S1',	'Vaughn1')
insert into log_in_id values('S2',	'William2')
insert into log_in_id values('S3',	'David3')
                             
--T4
--select * from log_in
insert into log_in values('ruby1',	123456789,'C')
insert into log_in values ('summer2', 123456790,'C')
insert into log_in values('devin3',	123456791,	'C')
insert into log_in values('Vaughn1',	123456792,	'S')
insert into log_in values('William2',123456793,	'S')
insert into log_in values('David3',	123456794,	'S')

--T5
--select * from user_type
insert into user_type values('Supplier','S')
insert into user_type values('Customer','C')
--T6
--select * from Customer_Address
insert into Customer_Address values('A1',	'C1','21b',	'Max Society',	416219)
insert into Customer_Address values('A2',	'C2',	'2a',	'Georgia Society', 411014)
insert into Customer_Address values('A3',	'C3',	'13c',	'Thomas Society',	400601)

--T7
select * from Supplier_Address
insert into Supplier_Address values('B1',	'S1',	'3a',	'Jose Society',	403602)
insert into Supplier_Address values('B2',	'S2',	'3b',	'Leon Society',	560037)
insert into Supplier_Address values('B3',   'S3',	'9c',	'Rebecca Society',	462016)

--T8 
select * from login_details
insert into login_details values('SS1',	'ruby1',	'13-08-2022 23:42:00',	'14-08-2022 23:42:00')
insert into login_details values('SS2',	'summer2',	'14-08-2022 23:42:00',	'15-08-2022 23:42:00')
insert into login_details values('SS3',	'devin3',	'15-08-2022 23:42:00',	'16-08-2022 23:42:00')

--T9
--select * from Country
insert into Country values(1,'India')
insert into Country values(2,	'US')
insert into Country values(3,	'England')

--T10
--select * from states
insert into states values('State1',	'Maharashtra',	1)
insert into states values('State2',	'Karnataka',	1)
insert into states values('State3',	'Goa',	1)
insert into states values('State4',	'Madhya Pradesh',	1)
insert into states values('State5',	'Andhra pradesh',	1)

--T11
--select * from district
insert into district values('D1',	'kolhapur',	'State1')
--insert into states values('D2',	'pune',	'State1')
--insert into states values('D3',	'Thane','State1')
insert into states values('D4',	'South Goa',	'State3')
insert into states values('D5',	'Banglore',	'State2')
insert into states values('D6', 'Bhopal',	'State4')
insert into states values('D7',	'Indore',	'State4')
insert into states values('D8','Visakhapatnam',	'State5')


--T12
--select * from Area 
insert into Area values(416219,	'Murgud',	'D1')
insert into Area values(411014,	'Punecity',	'D2')
insert into Area values(400601,	'Thane',	'D3')
insert into Area values(403602,	'Margao',	'D4')
insert into Area values(560037,	'Rameshnagar','D5')
insert into Area values(462016,	'Huzur',	'D6')
insert into Area values(452007,	'Gurunanak Chauk',	'D7')
insert into Area values(531115,	'Adakula',	'D8')

--T13 
--select * from Category
insert into Category values ('Cat1',	'Electronics') 
insert into Category values('Cat2',	'Books') 
insert into Category values('Cat3',	'Fashion') 

--T14
--select * from Sub_Category 
insert into Sub_Category values('Subcat1',	'TV',	'Cat1')
insert into Sub_Category values('Subcat2',	'Mobile',	'Cat1')
insert into Sub_Category values('Subcat3',	'AC',	'Cat1')
insert into Sub_Category values('Subcat4',	'comic books',	'Cat2')
insert into Sub_Category values('Subcat5',	'Autobiograpphy',	'Cat2')
insert into Sub_Category values('Subcat6',	'Selfhelp books',	'Cat2')
insert into Sub_Category values('Subcat7',	'Men',	'Cat3')
insert into Sub_Category values('Subcat8',	'Women',	'Cat3')
insert into Sub_Category values('Subcat9',	'Children',	'Cat3')



--T15
--select * from Product_Info
insert into Product_Info values ('TV_12',    'TV 32  inch',    '32 inch',    2,    1,    32000,    'LG',    'India',    7,    'Subcat1');
insert into Product_Info values ('Shirt1',    'Full sleeves Shirt',   'L',    0.2,    1,    1000,    'Arrow',    'India',    7,    'Subcat7');
insert into Product_Info values ('BK1',    'Automic Habits',   '300 pages',    0.5,    1,    500,    'Random House',    'India',    5,    'Subcat6');
insert into Product_Info values ('Shirt2',    'Half sleeves shirt',    'M',    0.2,    1,    700,    'Max',    'India',    5,    'Subcat7');
insert into Product_Info values ('AC1',    '1 ton AC',    '1 ton',    20,    1,    25000,    'Haier',    'India',    7,    'Subcat3');
insert into Product_Info values ('BK2',    'Long walk to freedom',    '200 pages',    0.5,    1,    500,    'Little Brown',    'India',    7,    'Subcat5');


--T16
insert into  stock values ('S1',	'TV_12',	10)
insert into  stock values('S1',	'Shirt1',	15)
insert into  stock values('S2',	'BK1',	10)
insert into  stock values('S2',	'Shirt2',	20)
insert into  stock values('S3',	'AC1',	20)
insert into  stock values('S3',	'BK2',	20)

--T17
insert into Order_Info values ('ORD_1',	'C1',	'15-06-2022',	'25-06-2022',	'ship1',	57600,	'15-06-2022',	'Complete')
insert into Order_Info values('ORD_2',	'C2',	'08-06-2022',	'18-06-2022',	'ship2',	1800,	'08-06-2022',	'Complete')
insert into Order_Info values('ORD_3',	'C3',	'01-06-2022',	'11-06-2022',	'ship3',	2160,	'01-06-2022',	'Complete')
--T18
insert into product_order1 values('PO1',	'S1',	'TV_12',	2,	1,	57600,	'ORD_1',	'Happy Birthday')
insert into product_order1 values('PO2',	'S2',	'Shirt1',	2,	1,	1800,	'ORD_2',	'Happy Anniversary')
insert into product_order1 values('PO3',	'S3',	'BK1',	2,	1,	900,	'ORD_3',	'Happy Birthday')
insert into product_order1 values('PO4',	'S1',	'Shirt2',	2,	1,	1260,	'ORD_3',	'Happy Anniversary')
--T20
insert into Payment values('ORD_1',	'Pay1',	1,	15-06-2022)
insert into Payment values('ORD_2',	'Pay2',	2,	08-06-2022)
insert into Payment values('ORD_3',	'Pay3',	3,	01-06-2022)
--T19
insert into Payment_Type values('COD',	'1')
insert into Payment_Type values('Internet Banking',	'2')
insert into Payment_Type values('UPI',	'3')
insert into Payment_Type values('Credit card',	'4')
insert into Payment_Type values('Debit card',	'5')
insert into Payment_Type values('Wallet',	'6')
--T21
insert into Supplier_PaymentType_details values('S1-1',	'S1',	'1')
insert into Supplier_PaymentType_details values('S1-2',	'S1',	'2')
insert into Supplier_PaymentType_details values('S1-3',	'S1',	'3')
insert into Supplier_PaymentType_details values('S2-2',	'S2',	'2')
insert into Supplier_PaymentType_details values('S2-3',	'S2',	'3')
insert into Supplier_PaymentType_details values('S2-4',	'S2',	'4')
--T22
insert into Shipment values('Ship1',	17-06-2022,	'Road',	'23-06-2022',	'Deliverd',	15-06-2022,	16-06-2022)
insert into Shipment values('Ship2',	10-06-2022,	'Road',	'16-06-2022',	'Deliverd',	08-06-2022,	09-06-2022)
insert into Shipment values('Ship3',	03-06-2022,	'Road',	'09-06-2022',	'Deliverd',	01-06-2022,	02-06-2022)



--T23
insert into Customer_BankDetails values ('C1',	987654321,	'HDFC Bank',	'HDFC1234',	123456789012,	123456912468,	'Ruby Patel')
insert into Customer_BankDetails values ('C2',	987654322,	'ICIC bank',	'ICICI1234',	234567890123,	234568013579,	'Summer Hayward')
insert into Customer_BankDetails values ('C3',	987654342,	'Kotak Mahindra bank',	'Kotak1234',	345678901234,	345679024690,	'Devin Huddleston')

--T24
--Select * from Supplier_bankdetails
insert into Supplier_bankdetails values('S1',	997654322,	'HDFC Bank',	'HDFC2345',	823456789082,	123456512468,'Vaughn')
insert into Supplier_bankdetails values('S2',	997654323,	'ICIC bank',	'ICICI2345',	234567890823,	234568013575,	'William')
insert into Supplier_bankdetails values('S3',	997654343,	'Kotak Mahindra bank',	'Kotak2345',	345678908234,	345675024650,	'David')

--T25
--Select * from Branch_details
insert into Branch_details values('Murgud',	'HDFC1234')
insert into Branch_details values('Punecity',	'ICICI1234')
insert into Branch_details values('Thane',	'Kotak1234')
insert into Branch_details values('Margao',	'HDFC2345')
insert into Branch_details values('Rameshnagar',	'ICICI2345')
insert into Branch_details values('Huzur',	'Kotak2345')
insert into Branch_details values('Gurunanak Chauk',	'HDFC3456')
insert into Branch_details values('Adakula',	'ICICI3456' )

--T26
Select * from UPI_Details
insert into UPI_Details values('C1',	'Ruby@hdfc.ac.in')
insert into UPI_Details values('C2',	'Summer@icici.ac.in')
insert into UPI_Details values('C3',	'Devin@kotak.ac.in')

--T27
Select * from review
insert into review values('TV_12',	4,	'Rev1',	17-06-2022,	'C1',	'Good product')
insert into review values('Shirt1',	5,	'Rev2',	10-06-2022,	'C2',	'Nice colour')
insert into review values('BK1',	4,	'Rev3',	03-06-2022,	'C3',	'Inspiring books')
insert into review values('Shirt2',	5,	'Rev4',	02-01-1900,	'C3',	'nice Fit')

--T28
Select * from Announcement
insert into Announcement values('Independence sale',	14-08-2022,	18-08-2022,	'Cat1',	'Upto 20%', 	'Desc1')
insert into Announcement values('Big Billion sale',	21-09-2022,	24-09-2022	,'Cat2',	'Upto 40%',	'Desc2')
insert into Announcement values('Year end Clearance sale',	20-12-2022,	24-12-2022,	'Cat3',	'Upto 25%',	'Desc3')

--T29
Select * from wishlist
insert into wishlist values('AC1',	'1 ton AC',	07-08-2022,	'C2')
insert into wishlist values('BK2',	'Long walk to freedom',	31-07-2022,	'C3')

--T30
select * from msg
insert into msg values('Msg_1',	'Delivery',	'Your order has been deliverd!!')
insert into msg values('Msg_2',	'Shipped',	'Your order has been Shipped!!')
insert into msg values('Msg_3',	'Packed',	'Your order is packed and ready to ship!!')

--T31
select * from notifications
insert into notifications values('C1',	'Msg_1',	'ORD_1',	23-06-2022,	'04:30:00',	'Notify1')
insert into notifications values('C2',	'Msg_2',	'ORD_2',	16-06-2022,	'04:30:00',	'Notify2')
insert into notifications values('C3',	'Msg_3',	'ORD_3',	09-06-2022,	'04:30:00',	'Notify3')

--T32
select * from Helpline
insert into Helpline values('IN',	111-222-3333)
insert into Helpline values('EN',	111-222-4444)
insert into Helpline values('US',	111-222-5555)
--T33
insert into cart_customer values('Cart_for_C1',	'C1')
insert into cart_customer values('Cart_for_C2',	'C2')
insert into cart_customer values('Cart_for_C3',	'C3')

--T34
insert into Discount values('1',	10%,	'UPI')
insert into Discount values('2',	12%,	'Credit card')
insert into Discount values('3',	8%,	'debit card')
--T35
insert into Cart values('Cart_for_C1',	'AC1',	2,	25000,	'1',	10%,	45000)
insert into Cart values('Cart_for_C1',	'BK2',	2,	500,	'2',	12%,	880)
insert into Cart values('Cart_for_C2',	'TV_12',	1,	32000,	'2',	12%,	28160)

--T36
select * from FAQ
insert into FAQ values('Q1',	'Can I return any product?	No, as per our company rule, no returns are possible due to covid 19 risk related to it')
insert into FAQ values('Q2',	'Is COD Possible?	For somesuppliers COD is possible')
insert into FAQ values('Q3',	'Do you offer protection against fraud?	Yes. We help you protect against fraudulent orders placed on your products and payment fraud.')

--T37
select * from Admin_info
insert into Admin_info values('admin1',	'Riddhi',	'passqwer')
insert into Admin_info values('admin2',	'Manasi',	'passtyuij')
insert into Admin_info values('admin3',	'Pratiksha','passoplkl')

--T38
select * from shipper
insert into shipper values('ritz',	'R_comp',	9867454363)
insert into shipper values('mansy',	'P_comp',	9867454364)
insert into shipper values('pratks','M_comp',	9867454365)

--T39
select * from service_center
insert into service_center values('Pune',	9234567780)
insert into service_center values('Mumbai',	9836353445)
insert into service_center values('Thane',	9836353447)


--T40
select * from clearance_warehouse
insert into clearance_warehouse values(1,	'dockyard',	'Margao')
insert into clearance_warehouse values(2,	'dexhouse',	'Ramesh nagar')
insert into clearance_warehouse values(3, 'shiatraders',	'Huzur')

