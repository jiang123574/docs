
```sh
/volume1/@appstore/transmission/bin/transmission-create -p -o /volume2/video/电视剧/Mindhunter.S02.1080p.NF.WEB-DL.DDP5.1.x264-MZABI.torrent -t http://hdhome.org/announce.php -s 2048 /volume2/video/电视剧/Mindhunter.S02.1080p.NF.WEB-DL.DDP5.1.x264-MZABI
```
参数
-p 表示这是私用的种子，这个必须要加上
-o 生成的种子输出位置，不要忘记把名字打上
-t tracker的地址，我用的家园的做范本，大家自行修改
-s 每个文件块的大小，单位是KB，我设置的是2M，也就是2048KB

