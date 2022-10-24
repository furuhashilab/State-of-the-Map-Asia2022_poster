# Submission guidelines
- Upload your poster through this [form](https://docs.google.com/forms/d/1J8nyBjI7FxAplLC91Cdi5XpO92XMSyWetNd1ASGxF60/viewform?edit_requested=true)
- Format: PDF
- Make sure to add a short description of the poster and indicate the mapping tools used
- Maximum file size: 50 MB
- Deadline: October 26, 2022

### Background
>Japanese

UN Vector Tile Toolkitは、UN Open GIS Initiativeの下で設計されたオープンソースツールのパッケージで、国連地理空間情報サービス、各国政府 地図機関などの公共ベースマップ提供者が最新のWebマッピング技術を活用してベースマップベクタルタイルを配信できるように設計されている。(Eom et al., 2017; M. A. Brovelli, 2021; UN Open GIS Initiative, 2022)。
 UNVT　Tile Toolkitは、様々なアプリケーションフレームワークで使用するための高速で相互運用可能なベースマップベクタールタイルを生成、ホスト、スタイル、最適化する既存の実績あるオープンソースソフトウェアがパッケージ化されている。(Fujimura et al., 2019, The United Nations Vector Tile Toolkit, 2022)
 UNVT Portableは、RaspberryPi用のパッケージで、ベクター/ラスタータイル地図のホスティングサーバーとして機能し、ローカルネットワーク内のWebブラウザから自由にアクセスすることができる。 主に激甚災害時のオフライン環境での機能を想定しており、災害危機対策本部が設置されている自治体で、ドローン空撮画像とOpenStreetMapや事前に用意された各種オープンデータを組み合わせてWebブラウザ上でオーバーレイ表示することが可能である。被災地全体の状況を効率的に把握し、迅速な救援・復興作業を可能にするユースケースでの活躍が期待される。
 
 > English
 
The UN Vector Tile Toolkit is a package of open source tools designed under the UN Open GIS Initiative to enable public basemap providers, such as the UN Geospatial Information Service and national government mapping agencies, to leverage the latest web mapping technology to It is designed to enable public basemap providers such as the United Nations Geospatial Information Service and national government mapping agencies to deliver basemap vector tiles using the latest web mapping technology. (Eom et al., 2017; M. A. Brovelli, 2021; UN Open GIS Initiative, 2022).
 The UNVT Tile Toolkit is packaged with existing proven open source software that generates, hosts, styles, and optimizes fast, interoperable basemap vector tiles for use in various application frameworks. (Fujimura et al., 2019, The United Nations Vector Tile Toolkit, 2022)
 UNVT Portable is a package for RaspberryPi that acts as a hosting server for vector/raster tile maps and can be freely accessed from a web browser in a local network. It is mainly intended to function in an offline environment in the event of a severe disaster. It is possible to combine drone aerial images with OpenStreetMap and various open data prepared in advance and overlay them on a Web browser in municipalities where disaster crisis headquarters have been established. The system is expected to play an active role in use cases to efficiently grasp the situation of the entire disaster area and enable prompt relief and reconstruction work.
 
 ### PURPOSE
>Japanese

本研究では、現在入手可能なRaspberryPi 4端末を想定し、OpenStreetMapをベースにプリインストールされたデータセットを構築し、OSMと相互に結合するストレージ方式や他のタイル型データセット等 パターン、ベースマップ、ドローン空撮データ、テーママッピング用の避難所・ハザードマップデータについてオープンデータとして入手できる適正ストレージ割り当てを算定する。また、外付けGPSレシーバーとExif（Exchangeable Image File Format）を用いて、オフライン環境下のRaspberryPi 4での位置情報取得の方法について検討する。

 > English
 
In this study, assuming currently available RaspberryPi 4 terminals, a pre-installed dataset based on OpenStreetMap will be constructed, and storage methods that interconnect with OSM and other tile-type datasets, etc. Pattern, basemap, drone aerial photography data, theme Calculate appropriate storage allocation available as open data for shelter and hazard map data for mapping. In addition, we will examine methods of acquiring location information on RaspberryPi 4 in an offline environment using an external GPS receiver and Exif (Exchangeable Image File Format).


 ### STRATEGY
 >Japanese
 
 私たちの研究グループでは、国内の複数の自治体と防災協定を締結し、大規模災害発生時にドローン空撮を迅速に提供するための情報支援活動を行っている。データ提供の過程では、提供先自治体の情報リテラシーや利用可能な端末の動作環境により、地理空間情報が必ずしも円滑に伝達されない現状がある。2019年の台風災害では大規模停電やインターネット停止などインフラが麻痺したため、オフライン環境でも適切に機能する使いやすいWeb地図のようなシステムが必要であると仮説を立て、実証実験を通じてその有効性を確認する。性能・コストともに比較的安価なRaspberryPiデバイスを前提に設計し、本研究で完成したUNVT Portable端末は将来起こりうる大規模自然災害に備えて自治体等に対し大量に配備していく予定である。
 
 > English
 
Our research group has concluded disaster management agreements with several municipalities in Japan and is engaged in information support activities to promptly provide drone aerial photography in the event of a large-scale disaster. In the process of data provision, geospatial information is not always smoothly communicated due to the information literacy of the recipient municipalities and the operating environment of available terminals; because the infrastructure was paralyzed by the typhoon disaster in 2019, including large-scale power outages and Internet outages, we have developed an easy-to-use, easy-to-use system that can function properly in an offline environment We hypothesize that a web map-like system that can function properly in an offline environment is needed, and will confirm its effectiveness through demonstration experiments. The UNVT Portable terminal completed in this research will be deployed in large numbers to local governments and other organizations in preparation for possible future large-scale natural disasters.

 ### DESIGN 
 
 > Japanese
 
Fujimura, 2019 が既に全世界のOpenStreetMapデータセットに対して有効な分割方法を提案しており、この方法は2022年現在でも有効である。RaspberryPi 4を前提に、搭載可能なMicroSDカードの容量や読み込み・描画速度の性能を比較評価し、一般的なChromebookの価格帯である300ドルの半額である150米ドルをコスト上限と定義する。ローカルネットワークの通信には、Wi-Fiを利用した無線接続を採用した。また、外付けのGPSレシーバーをRaspberryPi 4に接続させ、かつ外部からのExif付きの画像を取り込むことで、位置情報を取得させる。UNVT Portableとの接続は、QRコードによるWi-Fi自動接続機能を採用し、テーママップごとにQRコードを表示するなど、デジタル端末に不慣れな自治体職員でも簡単に地理空間情報にアクセスできるように設計されている。

> English

Fujimura, 2019 has already proposed a partitioning method that is valid for the worldwide OpenStreetMap dataset, and this method is still valid as of 2022; assuming a RaspberryPi 4, the capacity of the MicroSD card that can be installed and the performance of the reading and drawing speed are We evaluate and define the upper cost limit as US$150, half of the US$300 price range of a typical Chromebook. For local network communication, a Wi-Fi-based wireless connection was used. The UNVT Portable is connected to the RaspberryPi 4 by an automatic Wi-Fi connection using QR codes, and QR codes are displayed on each thematic map. The system is designed so that even municipal employees unfamiliar with digital terminals can easily access geospatial information, for example, by displaying a QR code for each thematic map.
 

 
 

 
 
