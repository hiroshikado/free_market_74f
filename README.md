# free_market_74f
フリマアプリのクローンサイト。


## usersテーブル

|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false|
|encrypted_password|string|null: false|
|reset_password_token|string||
|user_image|string||
|introduction|text||
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birth_day|date|null: false|

### Association
- has_many :buyer_records, class_name: 'Product', dependent: :destroy
- has_many :seller_records, class_name: 'Product', dependent: :destroy
- has_one :destination dependent: :destroy
- has_one :card dependent: :destroy
- has_many :comments dependent: :destroy


## destinationsテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kane|string|null: false|
|post_code|string|null: false|
|prefecture_id|integer|null: false|
|city|string|null: false|
|address|string|null: false|
|building_name|string||
|phone_number|string||


### Association
- belongs_to :user


## cardsテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|customer_id|string|null: false|
|card_id|string|null: false|

### Association
- belongs_to :user


## categoriesテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string||

### Association
- has_many :products
※ancestryは、gem ancestryを使用するため。


## productsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|price|integer|null: false|
|description|string|null: false|
|status|string|null: false|
|size|string|
|cost|string|null: false|
|days|string|null: false|
|prefecture_id|integer|null: false|
|judgment|string||
|category_id|references|null: false, foreign_key: true|
|brand|string|
|seller_id|references|null: false, foreign_key: : { to_table: :users }| 
|buyer_id|references｜foreign_key: { to_table: :users }|


### Association
- belongs_to :user, optional: true
- belongs_to :category, optional: true
- belongs_to :buyer, class_name: "User", optional: true, foreign_key: "buyer_id"
- belongs_to :seller, class_name: "User", optional: true, foreign_key: "seller_id"
- has_many :images dependent: :destroy
- accepts_nested_attributes_for :images,  allow_destroy: true
- belongs_to_active_hash :prefecture
- has_many :comments dependent: :destroy

## imagesテーブル

|Column|Type|Options|
|------|----|-------|
|image|string|null: false|
|product_id|integer|null: false, foreign_key: true|
|purchase_id|string|null: false, foreign_key: true|

### Association
- belongs_to :product


## brandsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string||

### Association
- has_many :products


## commentsテーブル

|Column|Type|Options|
|------|----|-------|
|product_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
|delete_check|integer|default: 0|
|comment|string||

### Association
- belongs_to :product
- belongs_to :user

## favoritesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|product_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :product
- belongs_to :user
