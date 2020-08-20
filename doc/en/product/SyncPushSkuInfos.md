## request
Request method | Request path
---|---
Post | http://product.skums.blsct.com/product/syncpushskuinfos

**Call instructions**
*  Please make sure that the SKU data is correct. Once the push is pushed, the subsequent push will not update.
*  If the push fails, please record the abnormal status code and verify the correctness of the abnormal status information.
*  Please do not push non-semantic content such as enumerations for some materials. Please convert the enumerations into copy content before pushing. This API does not exist to parse third-party enumeration fields.

# Request example
```json
curl -X POST  -H 'Content-Type:application/json' -H 'Authorization: bearer eyJhbGciOiJIUzI1NiJ9' --data '[
  {
        "SkuId":"20200815678",
        "GourpCode":"20200813",
        "Images":["http://img.blsct.com/14d4c58a-0893-4053-a395-9f5093c2ba0b.jpg","http://img.blsct.com/6cfb27e4-efcd-48e1-83b5-72d4485ec618.jpg"],
        "OriginalTitle":"宽松V领无袖T恤",
        "EnglishTitle":"Loose V-neck sleeveless T-shirt",
        "Weight":150,
        "Description":"200812_宽松V领无袖T恤上衣(货号6240)_酒红色_L",
        "Long":33,
        "Width":24,
        "Height":2.4,
        "Brand":"unbrand",
        "SupplierId":23456,
        "SupplierName":"广州百伦服装",
        "ValidPeriod":"2020-08-01",
        "ProductCharacter":[1,5,7],
        "VariationSpecificInfo":{"Color":"Blue"},
  }
]' http://product.skums.blsct.com/product/syncpushskuinfos
```
response json
```json
{
  "Message": "",
  "Code":100
}
```


#  Input parameter description
## ProSkuInfos DTO
parameter | type | required | example | field description
---|---|---|---|---
skuId|string|true|2020081317|SKU unique identifier
images|List&lt;string&gt; |true|["http://img.blsct.com/14d4c58a-0893-4053-a395-9f5093c2ba0b.jpg","http://img.blsct.com/6cfb27e4-efcd-48e1-83b5-72d4485ec618.jpg"]|SKU image URL collection
originalTitle|string|true|宽松V领无袖T恤 | SKU title(zh-cn) |
englishTitle|string|true|Loose V-neck sleeveless T-shirt| SKU title (en)|
weight|decimal|true|150 | SKU weight，Unit is g|
description|string|false|200812_宽松V领无袖T恤上衣(货号6240)_酒红色_L|Describe some basic information of SKU, no more than 500 characters|
long|decimal|true|33|SKU length，Unit is cm|
width|decimal|true|24|SKU width，Unit is cm|
height|decimal|true|2.4|SKU height，Unit is cm|
brand|String|false|unbrand|Mark what brand the current SKU belongs to|
supplierId|string|true|coupang 供应商id|Provide the coupang supplier id of the current SKU|
supplierName|string|true|Provide the supplier unit of the current SKU|
validPeriod|DateTime|false|2020-08-30|Expiration（**To be determined**）|
productCharacter|List&lt;int&gt;|true| [1,5,7] (Please refer to the corresponding table of ProductCharacterDto for the value)|Mark whether the current SKU has some special properties, such as: fragile items, knives, metals, flammable, etc.|
variationSpecificInfo|Dictionary&lt;string, string&gt;|false|{"Color":"Blue"}（**To be determined**）|Mark the attributes of the current SKU, such as: color, shape, model, etc.|

## Response parameter description 
Field | Type | Example | Description  
|---|---|---|---|
|message|string| xxx |Error message
|code|int|xxx|Status code (please refer to the status code description below)|

## Status code description
status code | Description |
---|---|
100|Request succeeded|
102|SkuId already exists|
111|Incorrect product property value|
140|Unable to get request parameters|
141|Required fields are missing|

## Product Nature Correspondence Table
### ProductCharacterDto 
value | text| desc
---|---|---
1	|no problem|
3	|With powder|Products with powder, powder-containing eye shadow cosmetics, makeup powder, nail velvet powder, plush powder and other products with powder, not pure powder
4	|Weapon self-defense|Self-defense weapons, such as defensive pens, card knives, etc.
5	|Fragile items|Easily damaged and broken, such as glass products, plastic products, etc.
7	|Supporting lithium ion 966|Battery and (used) equipment together, battery material: Li ION (lithium ion), such as ordinary mobile phones with external batteries, quadcopters, etc.
8	|Built-in lithium ion 967|The battery is in (used) equipment, battery material: Li ION (lithium ion), such as built-in battery mobile phone Iphone, smart watch, etc.
9	|Pure lithium ion 965|The main body of the product is a separate battery, the battery material: Li ION (lithium ion), such as mobile phone batteries, electronic cigarette MOD
10	|Tool|A product with a blade and a sharp edge that can cause personal injury. (Knifes with a blade over 10cm cannot be moved, spring automatic knives without thumb holes cannot be moved)
11	|mobile power|As long as it has a mobile power supply function, it can charge electronic devices (power bank)
12	|High-power battery(&gt;100w)|Products equipped with high-power batteries (power>100W) such as wheelbarrows, balance vehicles, and twisting vehicles
13	|Supporting lithium metal 969|Battery and (used) equipment together, battery material: Li Metal (lithium metal)
14	|Pure lithium metal 968|Separate battery, battery material: Li Metal (lithium metal)
15	|Built-in lithium metal 970|The battery is in (used) equipment, the battery material: Li Metal (lithium metal), such as (non-smart) electronic watches
17	|With cream|Products that are not easy to flow and have soft texture/high-viscosity products that need to be diluted before use, such as lipstick, solder paste, ballpoint pens, etc.
18	|Oily|Liquid and oily products, such as nail polish, nail glue, essential oil, gel pen, watercolor pen, signature pen, etc.
19	|With gas|Lighter gas or other
20	|With flammable solid|Flintstones, candles, magnesium tapes and other flammable products
21	|With Gelatinous|Products with high concentration or stickiness, such as glue, sticky paste, sheet mask, etc.
22	|Strong magnetic|If the maximum magnetic field strength measured at a distance of 2.1m (7ft) from the measured object exceeds 0.159A/m (200nt) for magnets, audio speakers, etc., this type is defined as strong magnetism, which is magnetic and can attract iron products or can deflect the compass. Removal or intact outer packaging surface can absorb the paper pin at any position, then the strong magnetic field can be defined
23	|Imitation brand|Without authorization, imitate international famous products. (Product appearance, shape, style, etc. are counterfeit, but their essence is indeed very different in material)
24	|Imitation|1. A counterfeit product imitated based on the original shape, material, and function of the imitation object; 2. A product that imitates the shape of some dangerous goods and sensitive products, but its product performance is commonly used in daily life. (Products that imitate the appearance of some dangerous goods sensitive products, such as U disk imitating grenade, imitating gun-shaped products)
25 | Imitation gun accessories | Gun accessories, holsters, strong sights, etc.
26 |Electronic Cigarette|Electronic Cigarette Products
27 |Wires|Wired earphones, data cables, conversion cables, HDMI cables and other cables containing metal. Products such as wired headsets, data cables, etc.
28 |Storage devices|Hard disks, U disks, TF cards, SD cards, tapes and all other devices that can store things.
29 |With liquid|Flowable and low-concentration products, such as refreshing lotion, refrigerant (<10ML)
30 |Other pure batteries|When the main body of the product is other types of batteries other than pure lithium ion batteries, pure lithium metal, and dry batteries
31 |Built-in dry battery|Dry battery belongs to the primary battery in the chemical power supply and is a kind of disposable battery. \t The battery is (used) in the device, that is, the battery is included in the product after the product is packaged and is defined as a built-in dry battery.
32 |Matched dry battery|Dry battery is a primary battery in chemical power supply and is a kind of disposable battery. The battery and (used) equipment together, that is, the battery and the product are stored separately and defined as a matching dry battery
33 | Atomizer | Electronic Cigarette Accessories
34 | E-cigarette | Electronic Cigarette Accessories
35 |MOD|Electronic cigarette accessories, such as temperature control box cigarettes, etc.
36 |Fragile products|Easily damaged, easily broken products, ceramic/glass products, tempered film, etc.
37 |Metal Parts| For all products with metal, choose this attribute regardless of size, such as: metal ornaments, screws, wrenches, pliers, multi-function tools, etc. (You don’t need to check the metal device when the battery attribute is checked in the product attribute)
38 |Laser|Laser pointer, laser engraving machine etc.
39 |Sexy products|Adult products, such as vibrators, airplane cups, etc.
40 |Infringement|1. Products whose trademark infringement has been confirmed, but there are no infringing trademarks and keywords on the product surface and packaging; 2. Unauthorized brand-name products, or product descriptions with brand-related sensitive words, such as Spiderman, Spiderman etc.
41 |Sensitive products|Products that are dangerous, special and easily intercepted by security checks, such as arc lighters and other imitation accessories with this function, quicksand mobile phone cases, hourglass products, and products containing activated carbon (such as water purifiers, Clean water bottle and other products with filtering function) etc.
42 |60CM<=L<=100CM|Package length is greater than or equal to 60 and less than or equal to 100CM.
43 |100CM<=L<=120CM|Package length is greater than or equal to 100 and less than or equal to 120CM.
44 |120CM<=L<=150CM|Package length is greater than or equal to 120 and less than or equal to 150CM.
45 |L>=150CM|Package length is greater than or equal to 150CM.
46 |Wood|Wooden products, such as wooden storage cabinets, building block toys, etc.
47 | Electronic Components | Xiawan Project Dedicated
48 | Pure Liquid | Products with a liquid content of more than 10ML
52 | Weak Magnetic|Magnetic but will not attract iron products or can not make the compass offset into weak magnetic, if the maximum magnetic field strength measured 2.1m (7ft) away from the measured object does not exceed 0.159A/m (200nt ), the article is not restricted as a magnetic substance and can be accepted and transported as ordinary goods. No paper clips can be adsorbed on the surface of the complete outer package, which is defined as ordinary goods
53 |Suspected dangerous goods|Suspected dangerous goods (with compressor products)
54 |Medical equipment|Medical equipment refers to instruments, equipment, appliances, materials or other items used on the human body alone or in combination, including professional medical equipment as well as household medical equipment.
56 |Slingshots|
142 |Built-in lithium ion with mobile power function|The built-in lithium ion battery of the product can be used as a mobile power source alone. Please check this category for multifunctional products that can charge other electronic devices, such as some camping lights
143 |Lead-acid battery|The electrode is mainly made of lead and its oxide, and the electrolyte is a kind of battery with sulfuric acid solution. English name: Lead-acid battery
147 |DA-Yes|
148 |DA-None|
