---
description: >-
  Day-to-Day lives we use different scanners and network-mappers to scan and map
  hosts. Here we look into how these things work , by creating a simple one for
  ourselves
---

# Scanner

## Requirements

We first need to define our requirements , what we need , how our code will work and how to proceed, we start by very basic ones We need out scanner to:

1. scan the open ports for a particular host
   1. TCP and UDP protocol
2. Grab the banner for the open ports
3. Scanner to be fast and reliable

### Start

First we need to understand that we need to have a way to deal with the ports that we need to scan for a host. Here I'm Using the Queue data-structure for that , which works like as it's name by letting the ports enter from one side , first-come-first-serve and the ports that get scanned are popped from the other side Here I defined 5 modes for the user to be able to use for our scanner:

1. mode 1 for starting 1024 ports
2. mode 2 for the starting 10000 ports
3. mode 3 for the top-ports for that particular protocol
4. mode all for the all ports
5. custom mode , only the specified ports by the user

### TCP and UDP mode:

We define by making a queue to load all the ports:

```python
from queue import Queue
queue = Queue()
```

we also define a function that takes user input and the desired ports by the user is loaded into the queue to be scanned:

we also define a function that takes user input and the desired ports by the user is loaded into the queue to be scanned: The function starts by basic conditionals of if-else where they define a above conditions , we enter the port to the queue by implementing the for loop.&#x20;

In the third mode I defined some top ports which had a higher probability of being open since they have the services assigned which are essential.

For the custom input , we call an `input` function which by default takes the `string input` , which then is passed to a `map` function which maps the integer function functionality to convert the ports given by the user to integer , but before that we also need to separate the ports by the space delimiter which is done by the `split()` function , if we want the delimiter to be comma we do: split(',').

Finally they are stored in a list which then looped over to put each port into queue.&#x20;

````python
```python
def tcp_mode(mode):
    if mode == 1:
        for port in range(1, 1025):
            queue.put(port)
    elif mode == 2:
        for port in range(1, 10001):
            queue.put(port)
    elif mode == 3:
        ports = [1, 3, 4, 6, 7, 9, 13, 17, 19, 20, 21, 22, 23, 24, 25, 26, 30, 32, 33, 37, 42, 43, 49, 53, 70, 79, 80, 81, 82, 83, 84, 85, 88, 89, 90, 99, 100, 106, 109, 110, 111, 113, 119, 125, 135, 139, 143, 144, 146, 161, 163, 179, 199, 211, 212, 222, 254, 255, 256, 259, 264, 280, 301, 306, 311, 340, 366, 389, 406, 407, 416, 417, 425, 427, 443, 444, 445, 458, 464, 465, 481, 497, 500, 512, 513, 514, 515, 524, 541, 543, 544, 545, 548, 554, 555, 563, 587, 593, 616, 617, 625, 631, 636, 646, 648, 666, 667, 668, 683, 687, 691, 700, 705, 711, 714, 720, 722, 726, 749, 765, 777, 783, 787, 800, 801, 808, 843, 873, 880, 888, 898, 900, 901, 902, 903, 911, 912, 981, 987, 990, 992, 993, 995, 999, 1000, 1001, 1002, 1007, 1009, 1010, 1011, 1021, 1022, 1023, 1024, 1025, 1026, 1027, 1028, 1029, 1030, 1031, 1032, 1033, 1034, 1035, 1036, 1037, 1038, 1039, 1040, 1041, 1042, 1043, 1044, 1045, 1046, 1047, 1048, 1049, 1050, 1051, 1052, 1053, 1054, 1055, 1056, 1057, 1058, 1059, 1060, 1061, 1062, 1063, 1064, 1065, 1066, 1067, 1068, 1069, 1070, 1071, 1072, 1073, 1074, 1075, 1076, 1077, 1078, 1079, 1080, 1081, 1082, 1083, 1084, 1085, 1086, 1087, 1088, 1089, 1090, 1091, 1092, 1093, 1094, 1095, 1096, 1097, 1098, 1099, 1100, 1102, 1104, 1105, 1106, 1107, 1108, 1110, 1111, 1112, 1113, 1114, 1117, 1119, 1121, 1122, 1123, 1124, 1126, 1130, 1131, 1132, 1137, 1138, 1141, 1145, 1147, 1148, 1149, 1151, 1152, 1154, 1163, 1164, 1165, 1166, 1169, 1174, 1175, 1183, 1185, 1186, 1187, 1192, 1198, 1199, 1201, 1213, 1216, 1217, 1218, 1233, 1234, 1236, 1244, 1247, 1248, 1259, 1271, 1272, 1277, 1287, 1296, 1300, 1301, 1309, 1310, 1311, 1322, 1328, 1334, 1337, 1352, 1417, 1433, 1434, 1443, 1455, 1461, 1494, 1500, 1501, 1503, 1521, 1524, 1533, 1556, 1580, 1583, 1594, 1600, 1641, 1658, 1666, 1687, 1688, 1700, 1717, 1718, 1719, 1720, 1721, 1723, 1755, 1761, 1782, 1783, 1801, 1805, 1812, 1839, 1840, 1862, 1863, 1864, 1875, 1900, 1914, 1935, 1947, 1971, 1972, 1974, 1984, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2013, 2020, 2021, 2022, 2030, 2033, 2034, 2035, 2038, 2040, 2041, 2042, 2043, 2045, 2046, 2047, 2048, 2049, 2065, 2068, 2099, 2100, 2103, 2105, 2106, 2107, 2111, 2119, 2121, 2126, 2135, 2144, 2160, 2161, 2170, 2179, 2190, 2191, 2196, 2200, 2222, 2251, 2260, 2288, 2301, 2323, 2366, 2381, 2382, 2383, 2393, 2394, 2399, 2401, 2492, 2500, 2522, 2525, 2557, 2601, 2602, 2604, 2605, 2607, 2608, 2638, 2701, 2702, 2710, 2717, 2718, 2725, 2800, 2809, 2811, 2869, 2875, 2909, 2910, 2920, 2967, 2968, 2998, 3000, 3001, 3003, 3005, 3006, 3007, 3011, 3013, 3017, 3030, 3031, 3052, 3071, 3077, 3128, 3168, 3211, 3221, 3260, 3261, 3268, 3269, 3283, 3300, 3301, 3306, 3322, 3323, 3324, 3325, 3333, 3351, 3367, 3369, 3370, 3371, 3372, 3389, 3390, 3404, 3476, 3493, 3517, 3527, 3546, 3551, 3580, 3659, 3689, 3690, 3703, 3737, 3766, 3784, 3800, 3801, 3809, 3814, 3826, 3827, 3828, 3851, 3869, 3871, 3878, 3880, 3889, 3905, 3914, 3918, 3920, 3945, 3971, 3986, 3995, 3998, 4000, 4001, 4002, 4003, 4004, 4005, 4006, 4045, 4111, 4125, 4126, 4129, 4224, 4242, 4279, 4321, 4343, 4443, 4444, 4445, 4446, 4449, 4550, 4567, 4662, 4848, 4899, 4900, 4998, 5000, 5001, 5002, 5003, 5004, 5009, 5030, 5033, 5050, 5051, 5054, 5060, 5061, 5080, 5087, 5100, 5101, 5102, 5120, 5190, 5200, 5214, 5221, 5222, 5225, 5226, 5269, 5280, 5298, 5357, 5405, 5414, 5431, 5432, 5440, 5500, 5510, 5544, 5550, 5555, 5560, 5566, 5631, 5633, 5666, 5678, 5679, 5718, 5730, 5800, 5801, 5802, 5810, 5811, 5815, 5822, 5825, 5850, 5859, 5862, 5877, 5900, 5901, 5902, 5903, 5904, 5906, 5907, 5910, 5911, 5915, 5922, 5925, 5950, 5952, 5959, 5960, 5961, 5962, 5963, 5987, 5988, 5989, 5998, 5999, 6000, 6001, 6002, 6003, 6004, 6005, 6006, 6007, 6009, 6025, 6059, 6100, 6101, 6106, 6112, 6123, 6129, 6156, 6346, 6389, 6502, 6510, 6543, 6547, 6565, 6566, 6567, 6580, 6646, 6666, 6667, 6668, 6669, 6689, 6692, 6699, 6779, 6788, 6789, 6792, 6839, 6881, 6901, 6969, 7000, 7001, 7002, 7004, 7007, 7019, 7025, 7070, 7100, 7103, 7106, 7200, 7201, 7402, 7435, 7443, 7496, 7512, 7625, 7627, 7676, 7741, 7777, 7778, 7800, 7911, 7920, 7921, 7937, 7938, 7999, 8000, 8001, 8002, 8007, 8008, 8009, 8010, 8011, 8021, 8022, 8031, 8042, 8045, 8080, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8093, 8099, 8100, 8180, 8181, 8192, 8193, 8194, 8200, 8222, 8254, 8290, 8291, 8292, 8300, 8333, 8383, 8400, 8402, 8443, 8500, 8600, 8649, 8651, 8652, 8654, 8701, 8800, 8873, 8888, 8899, 8994, 9000, 9001, 9002, 9003, 9009, 9010, 9011, 9040, 9050, 9071, 9080, 9081, 9090, 9091, 9099, 9100, 9101, 9102, 9103, 9110, 9111, 9200, 9207, 9220, 9290, 9415, 9418, 9485, 9500, 9502, 9503, 9535, 9575, 9593, 9594, 9595, 9618, 9666, 9876, 9877, 9878, 9898, 9900, 9917, 9929, 9943, 9944, 9968, 9998, 9999, 10000, 10001, 10002, 10003, 10004, 10009, 10010, 10012, 10024, 10025, 10082, 10180, 10215, 10243, 10566, 10616, 10617, 10621, 10626, 10628, 10629, 10778, 11110, 11111, 11967, 12000, 12174, 12265, 12345, 13456, 13722, 13782, 13783, 14000, 14238, 14441, 14442, 15000, 15002, 15003, 15004, 15660, 15742, 16000, 16001, 16012, 16016, 16018, 16080, 16113, 16992, 16993, 17877, 17988, 18040, 18101, 18988, 19101, 19283, 19315, 19350, 19780, 19801, 19842, 20000, 20005, 20031, 20221, 20222, 20828, 21571, 22939, 23502, 24444, 24800, 25734, 25735, 26214, 27000, 27352, 27353, 27355, 27356, 27715, 28201, 30000, 30718, 30951, 31038, 31337, 32768, 32769, 32770, 32771, 32772, 32773, 32774, 32775, 32776, 32777, 32778, 32779, 32780, 32781, 32782, 32783, 32784, 32785, 33354, 33899, 34571, 34572, 34573, 35500, 38292, 40193, 40911, 41511, 42510, 44176, 44442, 44443, 44501, 45100, 48080, 49152, 49153, 49154, 49155, 49156, 49157, 49158, 49159, 49160, 49161, 49163, 49165, 49167, 49175, 49176, 49400, 49999, 50000, 50001, 50002, 50003, 50006, 50300, 50389, 50500, 50636, 50800, 51103, 51493, 52673, 52822, 52848, 52869, 54045, 54328, 55055, 55056, 55555, 55600, 56737, 56738, 57294, 57797, 58080, 60020, 60443, 61532, 61900, 62078, 63331, 64623, 64680, 65000, 65129, 65389]

        for port in ports:
            queue.put(port)
    
    elif mode == 69:
        for port in range(1, 65535):
            queue.put(port)

    elif mode == 4:
        custom_ports = input("Enter custom ports separated by space: ")
        ports = list(map(int, custom_ports.split()))
        for port in ports:
            queue.put(port)
```
````

same for the UDP function:

````python
```python
def udp_mode(mode):
    if mode == 1:
        for port in range(1, 1025):
            queue.put(port)
    elif mode == 2:
        for port in range(1, 10001):
            queue.put(port)

    elif mode == 3:
        ports = [2,3,7,9,13,17,19,20,21,22,23,37,38,42,49,53,67,68,69,80,88,111,112,113,120,123,135,136,137,138,139,158,161,162,177,192,199,207,217,363,389,402,407,427,434,443,445,464,497,500,502,512,513,514,515,517,518,520,539,559,593,623,626,631,639,643,657,664,682,683,684,685,686,687,688,689,764,767,772,773,774,775,776,780,781,782,786,789,800,814,826,829,838,902,903,944,959,965,983,989,990,996,997,998,999,1000,1001,1007,1008,1012,1013,1014,1019,1020,1021,1022,1023,1024,1025,1026,1027,1028,1029,1030,1031,1032,1033,1034,1035,1036,1037,1038,1039,1040,1041,1042,1043,1044,1045,1046,1047,1048,1049,1050,1051,1053,1054,1055,1056,1057,1058,1059,1060,1064,1065,1066,1067,1068,1069,1070,1072,1080,1081,1087,1088,1090,1100,1101,1105,1124,1200,1214,1234,1346,1419,1433,1434,1455,1457,1484,1485,1524,1645,1646,1701,1718,1719,1761,1782,1804,1812,1813,1885,1886,1900,1901,1993,2000,2002,2048,2049,2051,2148,2160,2161,2222,2223,2343,2345,2362,2967,3052,3130,3283,3296,3343,3389,3401,3456,3457,3659,3664,3702,3703,4000,4008,4045,4444,4500,4666,4672,5000,5001,5002,5003,5010,5050,5060,5093,5351,5353,5355,5500,5555,5632,6000,6001,6002,6004,6050,6346,6347,6970,6971,7000,7938,8000,8001,8010,8181,8193,8900,9000,9001,9020,9103,9199,9200,9370,9876,9877,9950,10000,10080,11487,16086,16402,16420,16430,16433,16449,16498,16503,16545,16548,16573,16674,16680,16697,16700,16708,16711,16739,16766,16779,16786,16816,16829,16832,16838,16839,16862,16896,16912,16918,16919,16938,16939,16947,16948,16970,16972,16974,17006,17018,17077,17091,17101,17146,17184,17185,17205,17207,17219,17236,17237,17282,17302,17321,17331,17332,17338,17359,17417,17423,17424,17455,17459,17468,17487,17490,17494,17505,17533,17549,17573,17580,17585,17592,17605,17615,17616,17629,17638,17663,17673,17674,17683,17726,17754,17762,17787,17814,17823,17824,17836,17845,17888,17939,17946,17989,18004,18081,18113,18134,18156,18228,18234,18250,18255,18258,18319,18331,18360,18373,18449,18485,18543,18582,18605,18617,18666,18669,18676,18683,18807,18818,18821,18830,18832,18835,18869,18883,18888,18958,18980,18985,18987,18991,18994,18996,19017,19022,19039,19047,19075,19096,19120,19130,19140,19141,19154,19161,19165,19181,19193,19197,19222,19227,19273,19283,19294,19315,19322,19332,19374,19415,19482,19489,19500,19503,19504,19541,19600,19605,19616,19624,19625,19632,19639,19647,19650,19660,19662,19663,19682,19683,19687,19695,19707,19717,19718,19719,19722,19728,19789,19792,19933,19935,19936,19956,19995,19998,20003,20004,20019,20031,20082,20117,20120,20126,20129,20146,20154,20164,20206,20217,20249,20262,20279,20288,20309,20313,20326,20359,20360,20366,20380,20389,20409,20411,20423,20424,20425,20445,20449,20464,20465,20518,20522,20525,20540,20560,20665,20678,20679,20710,20717,20742,20752,20762,20791,20817,20842,20848,20851,20865,20872,20876,20884,20919,21000,21016,21060,21083,21104,21111,21131,21167,21186,21206,21207,21212,21247,21261,21282,21298,21303,21318,21320,21333,21344,21354,21358,21360,21364,21366,21383,21405,21454,21468,21476,21514,21524,21525,21556,21566,21568,21576,21609,21621,21625,21644,21649,21655,21663,21674,21698,21702,21710,21742,21780,21784,21800,21803,21834,21842,21847,21868,21898,21902,21923,21948,21967,22029,22043,22045,22053,22055,22105,22109,22123,22124,22341,22692,22695,22739,22799,22846,22914,22986,22996,23040,23176,23354,23531,23557,23608,23679,23781,23965,23980,24007,24279,24511,24594,24606,24644,24854,24910,25003,25157,25240,25280,25337,25375,25462,25541,25546,25709,25931,26407,26415,26720,26872,26966,27015,27195,27444,27473,27482,27707,27892,27899,28122,28369,28465,28493,28543,28547,28641,28840,28973,29078,29243,29256,29810,29823,29977,30263,30303,30365,30544,30656,30697,30704,30718,30975,31059,31073,31109,31189,31195,31335,31337,31365,31625,31681,31731,31891,32345,32385,32528,32768,32769,32770,32771,32772,32773,32774,32775,32776,32777,32778,32779,32780,32798,32815,32818,32931,33030,33249,33281,33354,33355,33459,33717,33744,33866,33872,34038,34079,34125,34358,34422,34433,34555,34570,34577,34578,34579,34580,34758,34796,34855,34861,34862,34892,35438,35702,35777,35794,36108,36206,36384,36458,36489,36669,36778,36893,36945,37144,37212,37393,37444,37602,37761,37783,37813,37843,38037,38063,38293,38412,38498,38615,39213,39217,39632,39683,39714,39723,39888,40019,40116,40441,40539,40622,40708,40711,40724,40732,40805,40847,40866,40915,41058,41081,41308,41370,41446,41524,41638,41702,41774,41896,41967,41971,42056,42172,42313,42431,42434,42508,42557,42577,42627,42639,43094,43195,43370,43514,43686,43824,43967,44101,44160,44179,44185,44190,44253,44334,44508,44923,44946,44968,45247,45380,45441,45685,45722,45818,45928,46093,46532,46836,47624,47765,47772,47808,47915,47981,48078,48189,48255,48455,48489,48761,49152,49153,49154,49155,49156,49157,49158,49159,49160,49161,49162,49163,49165,49166,49167,49168,49169,49170,49171,49172,49173,49174,49175,49176,49177,49178,49179,49180,49181,49182,49184,49185,49186,49187,49188,49189,49190,49191,49192,49193,49194,49195,49196,49197,49198,49199,49200,49201,49202,49204,49205,49207,49208,49209,49210,49211,49212,49213,49214,49215,49216,49220,49222,49226,49259,49262,49306,49350,49360,49393,49396,49503,49640,49968,50099,50164,50497,50612,50708,50919,51255,51456,51554,51586,51690,51717,51905,51972,52144,52225,52503,53006,53037,53571,53589,53838,54094,54114,54281,54321,54711,54807,54925,55043,55544,55587,56141,57172,57409,57410,57813,57843,57958,57977,58002,58075,58178,58419,58631,58640,58797,59193,59207,59765,59846,60172,60381,60423,61024,61142,61319,61322,61370,61412,61481,61550,61685,61961,62154,62287,62575,62677,62699,62958,63420,63555,64080,64481,64513,64590,64727,65024]
        for port in ports:
            queue.put(port)
    elif mode == 4:
        custom_ports = input("Enter custom ports separated by space: ")
        ports = list(map(int, custom_ports.split()))
        for port in ports:
            queue.put(port)
```
````

### Scanner function

Now since we have loaded al the ports into the queue , we need to scan them via the function that we're going to make

Here we start by defining the socket class's object and giving it some arguments:

1. socket.socket(AF\_INET,\<protocol which the user will choose>):
   1. AF\_INET defines the internet protocol family.
   2. \<protocol>:There are two in this case:
      1. SOCK\_STREAM: for the TCP  mode
      2. SOCK\_DGRAM: for the UDP mode

Then we connect to the port via `sock.connect_ex(())` function which takes the tuple as an input which contains the target ip and the port

If the function returns 0 meaning it was successfully connected else , the connection wasn't successful , and in any exception we say false

```python

def scan_port(protocol,port):
    try:
        # define a socket object with internet family class
        sock = socket.socket(socket.AF_INET, protocol)
        # setting a timeout
        sock.settimeout(1)
        # connect to the port for that target
        result = sock.connect_ex((target, port))
        # if the result is 0 that means no error
        if result == 0:
            return True
        return False
    # for any exception we say it wasn't successfull
    except Exception as e:
        return False

```

### Banner grabbing

Banner grabbing is a way to get the information from the port what's running on the other side , by connecting , and receiving the response

we start by again creating a scoket object to access the socket class's functions , now we are using the TCP mode for the banner grabbing due to the fact that TCP is much stable and responsible in packet handling

We start by connecting to the port , I just created a small condtion that if the port is 80 we need to deal with it differently as it requires different protocols , but no need if you don't want , we get the banner data by the function called `recv` which receives the specified bytes from the port it's connected to

```python
def banner_ip(banners, address, port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(10)  # Set a timeout of 10 seconds for the socket connection
    try:
        s.connect((address, port))
        if port == 80:
            print("\n" + Fore.GREEN + "[+] HTTP PROTOCOL Found" + Style.RESET_ALL + f" - IP: {address} | PORT: {port}\n")
            message = b"GET / HTTP/1.1\r\n\r\n"
            s.sendall(message)
        banner_data = s.recv(4096)
        if banner_data:
            banners.append([(address, port), banner_data.decode('utf-8')])
        else:
            print(Fore.YELLOW + f"[-] No response from IP: {address} | PORT: {port}" + Style.RESET_ALL+ "\n")
    except socket.timeout:
        print(Fore.YELLOW + f"[-] Connection timed out for IP: {address} | PORT: {port}" + Style.RESET_ALL + "\n")
    except socket.error as e:
        if e.errno == errno.ECONNREFUSED:
            pass
        else:
            print(Fore.RED + f"[-] Error connecting to IP: {address} | PORT: {port}" + Style.RESET_ALL)
    s.close()
```

### Faster with threading

Now we have everything :&#x20;

list of ports to scan , the mode to scan , the banner to grab , we just need to make this faster with threading , we can do this via implementing a worker function which will run by the help the multiple threads we'll be creating.

No complications, just looping through the queue and calling the scanner function we mentioned earlier

```python
def worker(protocol):
    while not queue.empty():
        port = queue.get()
        if scan_port(protocol, port):
            print(f"{'➣'*5} Port {Fore.GREEN} {port} {Style.RESET_ALL} is open")
            open_ports.append(port)
```

The run scanner function which calls threads as per the user's choice for the protocol

```python
def run_scanner(threads, mode, protocol):
    if protocol == socket.SOCK_STREAM:
        tcp_mode(mode)
    elif protocol == socket.SOCK_DGRAM:
        udp_mode(mode)
    else:
        print("Invalid choice !!!")
    thread_list = []
    for _ in range(threads):
        thread = threading.Thread(target=worker, args=(protocol,))
        thread_list.append(thread)

    for thread in thread_list:
        thread.start()

    for thread in thread_list:
        thread.join()

```



### Bonus:

I also added a little function and a dictionary that shows the information for the default services that run on the ports:

```python
port_info = {
    7: {
        "Service": "Echo",
        "Protocol": "TCP, UDP",
        "Description": "Echo service"
    },
    20: {
        "Service": "FTP-data",
        "Protocol": "TCP, SCTP",
        "Description": "File Transfer Protocol data transfer"
    },
    21: {
        "Service": "FTP",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "File Transfer Protocol (FTP) control connection"
    },
    22: {
        "Service": "SSH-SCP",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "Secure Shell, secure logins, file transfers (scp, sftp), and port forwarding"
    },
    23: {
        "Service": "Telnet",
        "Protocol": "TCP",
        "Description": "Telnet protocol—unencrypted text communications"
    },
    25: {
        "Service": "SMTP",
        "Protocol": "TCP",
        "Description": "Simple Mail Transfer Protocol, used for email routing between mail servers"
    },
    53: {
        "Service": "DNS",
        "Protocol": "TCP, UDP",
        "Description": "Domain Name System name resolver"
    # so on......
```

### Wrapping everything up

```python
print("Select a protocol:")
print("1. TCP")
print("2. UDP")
protocol_choice = int(input("Enter the protocol number (1 or 2): "))

if protocol_choice == 1:
    run_scanner(200, int(input("Select a mode: 1 for 1024, 2 for 10000, 3 for common ports, 69 for all ,4 for custom: ")), socket.SOCK_STREAM)
elif protocol_choice == 2:
    run_scanner(200, int(input("Select a mode: 1 for 1024, 2 for 10000, 3 for common ports, 4 for custom: ")), socket.SOCK_DGRAM)
else:
    print("Invalid protocol choice. Please select 1 or 2 for TCP or UDP.")

print(f"{'➣'*5} Port scan complete {'➣'*5}\n")
print(Fore.GREEN + f"{'➣'*5} Info for these ports (Note: This information is predefined and may not be accurate for all use cases):" + Style.RESET_ALL+"\n")

# Iterate through the list of ports
for port in open_ports:
    if port in port_info:
        info = port_info[port]
        print(f"🢂 {Fore.CYAN}Port: {port} | Service: {info['Service']} | Protocol: {info['Protocol']} | Description: {info['Description']}{Style.RESET_ALL}\n")
    else:
        print(f"{Fore.RED}Port {port} not found in the dictionary{Style.RESET_ALL}\n")
print(f"{'➣'*5} Attempting the banner grabbing now: {'➣'*5}\n")
banners = []
for port in open_ports:
    banner_ip(banners, target, port)
for banner in banners:
    print(Fore.CYAN + f"BANNER for IP: {banner[0][0]} | PORT: {banner[0][1]}" + Style.RESET_ALL)
    print(f"🏁  ->  \n {banner[1]}")
    print(f"         -------------------------------------------------------------------------------------------      \n")
```



## Whole code

```python
import socket
from queue import Queue
import threading
from colorama import Fore, Style
import errno
import requests

# Define a nested dictionary to store port information
port_info = {
    7: {
        "Service": "Echo",
        "Protocol": "TCP, UDP",
        "Description": "Echo service"
    },
    20: {
        "Service": "FTP-data",
        "Protocol": "TCP, SCTP",
        "Description": "File Transfer Protocol data transfer"
    },
    21: {
        "Service": "FTP",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "File Transfer Protocol (FTP) control connection"
    },
    22: {
        "Service": "SSH-SCP",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "Secure Shell, secure logins, file transfers (scp, sftp), and port forwarding"
    },
    23: {
        "Service": "Telnet",
        "Protocol": "TCP",
        "Description": "Telnet protocol—unencrypted text communications"
    },
    25: {
        "Service": "SMTP",
        "Protocol": "TCP",
        "Description": "Simple Mail Transfer Protocol, used for email routing between mail servers"
    },
    53: {
        "Service": "DNS",
        "Protocol": "TCP, UDP",
        "Description": "Domain Name System name resolver"
    },
    69: {
        "Service": "TFTP",
        "Protocol": "UDP",
        "Description": "Trivial File Transfer Protocol"
    },
    80: {
        "Service": "HTTP",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "Hypertext Transfer Protocol (HTTP) uses TCP in versions 1.x and 2. HTTP/3 uses QUIC, a transport protocol on top of UDP"
    },
    88: {
        "Service": "Kerberos",
        "Protocol": "TCP, UDP",
        "Description": "Network authentication system"
    },
    102: {
        "Service": "Iso-tsap",
        "Protocol": "TCP",
        "Description": "ISO Transport Service Access Point (TSAP) Class 0 protocol"
    },
    110: {
        "Service": "POP3",
        "Protocol": "TCP",
        "Description": "Post Office Protocol, version 3 (POP3)"
    },
    111: {
        "Service": "Sun-RPC",
        "Protocol": "TCP, UDP",
        "Description": "Port 111 was designed by the Sun Microsystems as a component of their Network File System"
    }
    ,
    135: {
        "Service": "Microsoft EPMAP",
        "Protocol": "TCP, UDP",
        "Description": "Microsoft EPMAP (End Point Mapper), also known as DCE/RPC Locator service, used to remotely manage services including DHCP server, DNS server, and WINS. Also used by DCOM"
    },
    137: {
        "Service": "NetBIOS-ns",
        "Protocol": "TCP, UDP",
        "Description": "NetBIOS Name Service, used for name registration and resolution"
    },
    139: {
        "Service": "NetBIOS-ssn",
        "Protocol": "TCP, UDP",
        "Description": "NetBIOS Session Service"
    },
    143: {
        "Service": "IMAP4",
        "Protocol": "TCP, UDP",
        "Description": "Internet Message Access Protocol (IMAP), management of electronic mail messages on a server"
    },
    381: {
        "Service": "HP Openview",
        "Protocol": "TCP, UDP",
        "Description": "HP data alarm manager"
    },
    383: {
        "Service": "HP Openview",
        "Protocol": "TCP, UDP",
        "Description": "HP performance data collector."
    },
    443: {
        "Service": "HTTP over SSL",
        "Protocol": "TCP, UDP, SCTP",
        "Description": "Hypertext Transfer Protocol Secure (HTTPS) uses TCP in versions 1.x and 2. HTTP/3 uses QUIC, a transport protocol on top of UDP."
    },
    445: {
        "Service": "microsoft-ds",
        "Protocol": "TCP",
        "Description": "The SMB (Server Message Block) protocol is used for file sharing in Windows NT/2K/XP and later"
    },
    464: {
        "Service": "Kerberos",
        "Protocol": "TCP, UDP",
        "Description": "Kerberos Change/Set password"
    },
    465: {
        "Service": "SMTP over TLS/SSL, SSM",
        "Protocol": "TCP",
        "Description": "Authenticated SMTP over TLS/SSL (SMTPS), URL Rendezvous Directory for SSM (Cisco protocol)"
    },
    587: {
        "Service": "SMTP",
        "Protocol": "TCP",
        "Description": "Email message submission"
    },
    593: {
        "Service": "Microsoft DCOM",
        "Protocol": "TCP, UDP",
        "Description": "HTTP RPC Ep Map, Remote procedure call over Hypertext Transfer Protocol, often used by Distributed Component Object Model services and Microsoft Exchange Server"
    },
    636: {
        "Service": "LDAP over TLS/SSL",
        "Protocol": "TCP, UDP",
        "Description": "Lightweight Directory Access Protocol over TLS/SSL"
    },
    691: {
        "Service": "MS Exchange",
        "Protocol": "TCP",
        "Description": "MS Exchange Routing"
    },
    902: {
        "Service": "VMware Server (unofficial)",
        "Protocol": "UDP",
        "Description": "VMware ESXi"
    },
    989: {
        "Service": "FTP over SSL",
        "Protocol": "TCP, UDP",
        "Description": "FTPS Protocol (data), FTP over TLS/SSL"
    },
    990: {
        "Service": "FTP over SSL",
        "Protocol": "TCP, UDP",
        "Description": "FTPS Protocol (control), FTP over TLS/SSL"
    },
    993: {
        "Service": "IMAP4 over SSL",
        "Protocol": "TCP",
        "Description": "Internet Message Access Protocol over TLS/SSL (IMAPS)"
    },
    995: {
        "Service": "POP3 over SSL",
        "Protocol": "TCP, UDP",
        "Description": "Post Office Protocol 3 over TLS/SSL"
    },
    1025: {
        "Service": "Microsoft RPC",
        "Protocol": "TCP",
        "Description": "Microsoft operating systems tend to allocate one or more unsuspected, publicly exposed services (probably DCOM, but who knows) among the first handful of ports immediately above the end of the service port range (1024+)."
    },
    1194: {
        "Service": "OpenVPN",
        "Protocol": "TCP, UDP",
        "Description": "OpenVPN"
    },
    1337: {
        "Service": "WASTE (unofficial)",
        "Protocol": "WASTE Encrypted File Sharing Program"
    },
    1589: {
        "Service": "Cisco VQP",
        "Protocol": "TCP, UDP",
        "Description": "Cisco VLAN Query Protocol (VQP)"
    },
    1725: {
        "Service": "Steam",
        "Protocol": "UDP",
        "Description": "Valve Steam Client uses port 1725"
    },
    2049: {
        "Service": "NFS",
        "Protocol": "tcp,udp,sctp",
        "Description": "Network File System (NFS) - remote filesystem access - A commonly scanned and exploited attack vector. Normally, port scanning is needed to find which port this service runs on"
    },
    2082: {
        "Service": "cPanel (unofficial)",
        "Protocol": "cPanel default"
    },
    2083: {
        "Service": "radsec, cPanel",
        "Protocol": "TCP, UDP",
        "Description": "Secure RADIUS Service (radsec), cPanel default SSL"
    },
    2483: {
        "Service": "Oracle DB",
        "Protocol": "TCP, UDP",
        "Description": "Oracle database listening for insecure client connections to the listener, replaces port 1521"
    },
    2484: {
        "Service": "Oracle DB",
        "Protocol": "TCP, UDP",
        "Description": "Oracle database listening for SSL client connections to the listener"
    },
    2967: {
        "Service": "Symantec AV",
        "Protocol": "TCP, UDP",
        "Description": "Symantec System Center agent (SSC-AGENT)"
    },
    3074: {
        "Service": "XBOX Live",
        "Protocol": "TCP, UDP",
        "Description": "Xbox LIVE and Games for Windows – Live"
    },
    3306: {
        "Service": "MySQL",
        "Protocol": "TCP",
        "Description": "MySQL database system"
    },
    3389: {
        "Service": "Windows remote desktop",
        "Protocol": "TCP",
        "Description": " used for Windows Remote Desktop and Remote Assistance connections (RDP - Remote Desktop Protocol). Also used by Windows Terminal Server"
    },

    3724: {
        "Service": "World of Warcraft",
        "Protocol": "TCP, UDP",
        "Description": "Some Blizzard games, Unofficial Club Penguin Disney online game for kids"
    },

    4664: {
        "Service": "Google Desktop (unofficial)",
        "Protocol": "Google Desktop Search"
    },
    5432: {
        "Service": "PostgreSQL",
        "Protocol": "TCP",
        "Description": "PostgreSQL database system"
    },
    5900: {
        "Service": "RFB/VNC Server",
        "Protocol": "TCP, UDP",
        "Description": "Virtual Network Computing (VNC) Remote Frame Buffer RFB protocol"
    },
    "6665-6669": {
        "Service": "IRC",
        "Protocol": "TCP",
        "Description": "Internet Relay Chat"
    },
    6881: {
        "Service": "BitTorrent (unofficial)",
        "Protocol": "BitTorrent is part of the full range of ports used most often"
    },
    6999: {
        "Service": "BitTorrent (unofficial)",
        "Protocol": "BitTorrent is part of the full range of ports used most often"
    },
    6970: {
        "Service": "Quicktime (unofficial)",
        "Protocol": "QuickTime Streaming Server"
    },
    8086: {
        "Service": "Kaspersky AV",
        "Protocol": "TCP",
        "Description": "Kaspersky AV Control Center"
    },
    8087: {
        "Service": "Kaspersky AV",
        "Protocol": "UDP",
        "Description": "Kaspersky AV Control Center"
    },
    8222: {
        "Service": "VMware Server",
        "Protocol": "TCP, UDP",
        "Description": "VMware Server Management User Interface (insecure Web interface)."
    },
    9100: {
        "Service": "PDL",
        "Protocol": "TCP",
        "Description": "PDL Data Stream, used for printing to certain network printers."
    },
    10000: {
        "Service": "BackupExec (unofficial)",
        "Protocol": "Webmin, Web-based Unix/Linux system administration tool (default port)"
    },
    12345: {
        "Service": "NetBus (unofficial)",
        "Protocol": "NetBus remote administration tool (often Trojan horse)."
    },
    27374: {
        "Service": "Sub7 (unofficial)",
        "Protocol": "Sub7 default"
    },
    31337: {
        "Service": "Back Orifice (unofficial)",
        "Protocol": "Back Orifice 2000 remote administration tools"
    }
}

target = input("the target: ")
queue = Queue()
open_ports = []
# function to populate the queue and get the mode
def tcp_mode(mode):
    if mode == 1:
        for port in range(1, 1025):
            queue.put(port)
    elif mode == 2:
        for port in range(1, 10001):
            queue.put(port)
    elif mode == 3:
        ports = [1, 3, 4, 6, 7, 9, 13, 17, 19, 20, 21, 22, 23, 24, 25, 26, 30, 32, 33, 37, 42, 43, 49, 53, 70, 79, 80, 81, 82, 83, 84, 85, 88, 89, 90, 99, 100, 106, 109, 110, 111, 113, 119, 125, 135, 139, 143, 144, 146, 161, 163, 179, 199, 211, 212, 222, 254, 255, 256, 259, 264, 280, 301, 306, 311, 340, 366, 389, 406, 407, 416, 417, 425, 427, 443, 444, 445, 458, 464, 465, 481, 497, 500, 512, 513, 514, 515, 524, 541, 543, 544, 545, 548, 554, 555, 563, 587, 593, 616, 617, 625, 631, 636, 646, 648, 666, 667, 668, 683, 687, 691, 700, 705, 711, 714, 720, 722, 726, 749, 765, 777, 783, 787, 800, 801, 808, 843, 873, 880, 888, 898, 900, 901, 902, 903, 911, 912, 981, 987, 990, 992, 993, 995, 999, 1000, 1001, 1002, 1007, 1009, 1010, 1011, 1021, 1022, 1023, 1024, 1025, 1026, 1027, 1028, 1029, 1030, 1031, 1032, 1033, 1034, 1035, 1036, 1037, 1038, 1039, 1040, 1041, 1042, 1043, 1044, 1045, 1046, 1047, 1048, 1049, 1050, 1051, 1052, 1053, 1054, 1055, 1056, 1057, 1058, 1059, 1060, 1061, 1062, 1063, 1064, 1065, 1066, 1067, 1068, 1069, 1070, 1071, 1072, 1073, 1074, 1075, 1076, 1077, 1078, 1079, 1080, 1081, 1082, 1083, 1084, 1085, 1086, 1087, 1088, 1089, 1090, 1091, 1092, 1093, 1094, 1095, 1096, 1097, 1098, 1099, 1100, 1102, 1104, 1105, 1106, 1107, 1108, 1110, 1111, 1112, 1113, 1114, 1117, 1119, 1121, 1122, 1123, 1124, 1126, 1130, 1131, 1132, 1137, 1138, 1141, 1145, 1147, 1148, 1149, 1151, 1152, 1154, 1163, 1164, 1165, 1166, 1169, 1174, 1175, 1183, 1185, 1186, 1187, 1192, 1198, 1199, 1201, 1213, 1216, 1217, 1218, 1233, 1234, 1236, 1244, 1247, 1248, 1259, 1271, 1272, 1277, 1287, 1296, 1300, 1301, 1309, 1310, 1311, 1322, 1328, 1334, 1337, 1352, 1417, 1433, 1434, 1443, 1455, 1461, 1494, 1500, 1501, 1503, 1521, 1524, 1533, 1556, 1580, 1583, 1594, 1600, 1641, 1658, 1666, 1687, 1688, 1700, 1717, 1718, 1719, 1720, 1721, 1723, 1755, 1761, 1782, 1783, 1801, 1805, 1812, 1839, 1840, 1862, 1863, 1864, 1875, 1900, 1914, 1935, 1947, 1971, 1972, 1974, 1984, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2013, 2020, 2021, 2022, 2030, 2033, 2034, 2035, 2038, 2040, 2041, 2042, 2043, 2045, 2046, 2047, 2048, 2049, 2065, 2068, 2099, 2100, 2103, 2105, 2106, 2107, 2111, 2119, 2121, 2126, 2135, 2144, 2160, 2161, 2170, 2179, 2190, 2191, 2196, 2200, 2222, 2251, 2260, 2288, 2301, 2323, 2366, 2381, 2382, 2383, 2393, 2394, 2399, 2401, 2492, 2500, 2522, 2525, 2557, 2601, 2602, 2604, 2605, 2607, 2608, 2638, 2701, 2702, 2710, 2717, 2718, 2725, 2800, 2809, 2811, 2869, 2875, 2909, 2910, 2920, 2967, 2968, 2998, 3000, 3001, 3003, 3005, 3006, 3007, 3011, 3013, 3017, 3030, 3031, 3052, 3071, 3077, 3128, 3168, 3211, 3221, 3260, 3261, 3268, 3269, 3283, 3300, 3301, 3306, 3322, 3323, 3324, 3325, 3333, 3351, 3367, 3369, 3370, 3371, 3372, 3389, 3390, 3404, 3476, 3493, 3517, 3527, 3546, 3551, 3580, 3659, 3689, 3690, 3703, 3737, 3766, 3784, 3800, 3801, 3809, 3814, 3826, 3827, 3828, 3851, 3869, 3871, 3878, 3880, 3889, 3905, 3914, 3918, 3920, 3945, 3971, 3986, 3995, 3998, 4000, 4001, 4002, 4003, 4004, 4005, 4006, 4045, 4111, 4125, 4126, 4129, 4224, 4242, 4279, 4321, 4343, 4443, 4444, 4445, 4446, 4449, 4550, 4567, 4662, 4848, 4899, 4900, 4998, 5000, 5001, 5002, 5003, 5004, 5009, 5030, 5033, 5050, 5051, 5054, 5060, 5061, 5080, 5087, 5100, 5101, 5102, 5120, 5190, 5200, 5214, 5221, 5222, 5225, 5226, 5269, 5280, 5298, 5357, 5405, 5414, 5431, 5432, 5440, 5500, 5510, 5544, 5550, 5555, 5560, 5566, 5631, 5633, 5666, 5678, 5679, 5718, 5730, 5800, 5801, 5802, 5810, 5811, 5815, 5822, 5825, 5850, 5859, 5862, 5877, 5900, 5901, 5902, 5903, 5904, 5906, 5907, 5910, 5911, 5915, 5922, 5925, 5950, 5952, 5959, 5960, 5961, 5962, 5963, 5987, 5988, 5989, 5998, 5999, 6000, 6001, 6002, 6003, 6004, 6005, 6006, 6007, 6009, 6025, 6059, 6100, 6101, 6106, 6112, 6123, 6129, 6156, 6346, 6389, 6502, 6510, 6543, 6547, 6565, 6566, 6567, 6580, 6646, 6666, 6667, 6668, 6669, 6689, 6692, 6699, 6779, 6788, 6789, 6792, 6839, 6881, 6901, 6969, 7000, 7001, 7002, 7004, 7007, 7019, 7025, 7070, 7100, 7103, 7106, 7200, 7201, 7402, 7435, 7443, 7496, 7512, 7625, 7627, 7676, 7741, 7777, 7778, 7800, 7911, 7920, 7921, 7937, 7938, 7999, 8000, 8001, 8002, 8007, 8008, 8009, 8010, 8011, 8021, 8022, 8031, 8042, 8045, 8080, 8081, 8082, 8083, 8084, 8085, 8086, 8087, 8088, 8089, 8090, 8093, 8099, 8100, 8180, 8181, 8192, 8193, 8194, 8200, 8222, 8254, 8290, 8291, 8292, 8300, 8333, 8383, 8400, 8402, 8443, 8500, 8600, 8649, 8651, 8652, 8654, 8701, 8800, 8873, 8888, 8899, 8994, 9000, 9001, 9002, 9003, 9009, 9010, 9011, 9040, 9050, 9071, 9080, 9081, 9090, 9091, 9099, 9100, 9101, 9102, 9103, 9110, 9111, 9200, 9207, 9220, 9290, 9415, 9418, 9485, 9500, 9502, 9503, 9535, 9575, 9593, 9594, 9595, 9618, 9666, 9876, 9877, 9878, 9898, 9900, 9917, 9929, 9943, 9944, 9968, 9998, 9999, 10000, 10001, 10002, 10003, 10004, 10009, 10010, 10012, 10024, 10025, 10082, 10180, 10215, 10243, 10566, 10616, 10617, 10621, 10626, 10628, 10629, 10778, 11110, 11111, 11967, 12000, 12174, 12265, 12345, 13456, 13722, 13782, 13783, 14000, 14238, 14441, 14442, 15000, 15002, 15003, 15004, 15660, 15742, 16000, 16001, 16012, 16016, 16018, 16080, 16113, 16992, 16993, 17877, 17988, 18040, 18101, 18988, 19101, 19283, 19315, 19350, 19780, 19801, 19842, 20000, 20005, 20031, 20221, 20222, 20828, 21571, 22939, 23502, 24444, 24800, 25734, 25735, 26214, 27000, 27352, 27353, 27355, 27356, 27715, 28201, 30000, 30718, 30951, 31038, 31337, 32768, 32769, 32770, 32771, 32772, 32773, 32774, 32775, 32776, 32777, 32778, 32779, 32780, 32781, 32782, 32783, 32784, 32785, 33354, 33899, 34571, 34572, 34573, 35500, 38292, 40193, 40911, 41511, 42510, 44176, 44442, 44443, 44501, 45100, 48080, 49152, 49153, 49154, 49155, 49156, 49157, 49158, 49159, 49160, 49161, 49163, 49165, 49167, 49175, 49176, 49400, 49999, 50000, 50001, 50002, 50003, 50006, 50300, 50389, 50500, 50636, 50800, 51103, 51493, 52673, 52822, 52848, 52869, 54045, 54328, 55055, 55056, 55555, 55600, 56737, 56738, 57294, 57797, 58080, 60020, 60443, 61532, 61900, 62078, 63331, 64623, 64680, 65000, 65129, 65389]

        for port in ports:
            queue.put(port)
    
    elif mode == 69:
        for port in range(1, 65535):
            queue.put(port)

    elif mode == 4:
        custom_ports = input("Enter custom ports separated by space: ")
        ports = list(map(int, custom_ports.split()))
        for port in ports:
            queue.put(port)

def udp_mode(mode):
    if mode == 1:
        for port in range(1, 1025):
            queue.put(port)
    elif mode == 2:
        for port in range(1, 10001):
            queue.put(port)

    elif mode == 3:
        ports = [2,3,7,9,13,17,19,20,21,22,23,37,38,42,49,53,67,68,69,80,88,111,112,113,120,123,135,136,137,138,139,158,161,162,177,192,199,207,217,363,389,402,407,427,434,443,445,464,497,500,502,512,513,514,515,517,518,520,539,559,593,623,626,631,639,643,657,664,682,683,684,685,686,687,688,689,764,767,772,773,774,775,776,780,781,782,786,789,800,814,826,829,838,902,903,944,959,965,983,989,990,996,997,998,999,1000,1001,1007,1008,1012,1013,1014,1019,1020,1021,1022,1023,1024,1025,1026,1027,1028,1029,1030,1031,1032,1033,1034,1035,1036,1037,1038,1039,1040,1041,1042,1043,1044,1045,1046,1047,1048,1049,1050,1051,1053,1054,1055,1056,1057,1058,1059,1060,1064,1065,1066,1067,1068,1069,1070,1072,1080,1081,1087,1088,1090,1100,1101,1105,1124,1200,1214,1234,1346,1419,1433,1434,1455,1457,1484,1485,1524,1645,1646,1701,1718,1719,1761,1782,1804,1812,1813,1885,1886,1900,1901,1993,2000,2002,2048,2049,2051,2148,2160,2161,2222,2223,2343,2345,2362,2967,3052,3130,3283,3296,3343,3389,3401,3456,3457,3659,3664,3702,3703,4000,4008,4045,4444,4500,4666,4672,5000,5001,5002,5003,5010,5050,5060,5093,5351,5353,5355,5500,5555,5632,6000,6001,6002,6004,6050,6346,6347,6970,6971,7000,7938,8000,8001,8010,8181,8193,8900,9000,9001,9020,9103,9199,9200,9370,9876,9877,9950,10000,10080,11487,16086,16402,16420,16430,16433,16449,16498,16503,16545,16548,16573,16674,16680,16697,16700,16708,16711,16739,16766,16779,16786,16816,16829,16832,16838,16839,16862,16896,16912,16918,16919,16938,16939,16947,16948,16970,16972,16974,17006,17018,17077,17091,17101,17146,17184,17185,17205,17207,17219,17236,17237,17282,17302,17321,17331,17332,17338,17359,17417,17423,17424,17455,17459,17468,17487,17490,17494,17505,17533,17549,17573,17580,17585,17592,17605,17615,17616,17629,17638,17663,17673,17674,17683,17726,17754,17762,17787,17814,17823,17824,17836,17845,17888,17939,17946,17989,18004,18081,18113,18134,18156,18228,18234,18250,18255,18258,18319,18331,18360,18373,18449,18485,18543,18582,18605,18617,18666,18669,18676,18683,18807,18818,18821,18830,18832,18835,18869,18883,18888,18958,18980,18985,18987,18991,18994,18996,19017,19022,19039,19047,19075,19096,19120,19130,19140,19141,19154,19161,19165,19181,19193,19197,19222,19227,19273,19283,19294,19315,19322,19332,19374,19415,19482,19489,19500,19503,19504,19541,19600,19605,19616,19624,19625,19632,19639,19647,19650,19660,19662,19663,19682,19683,19687,19695,19707,19717,19718,19719,19722,19728,19789,19792,19933,19935,19936,19956,19995,19998,20003,20004,20019,20031,20082,20117,20120,20126,20129,20146,20154,20164,20206,20217,20249,20262,20279,20288,20309,20313,20326,20359,20360,20366,20380,20389,20409,20411,20423,20424,20425,20445,20449,20464,20465,20518,20522,20525,20540,20560,20665,20678,20679,20710,20717,20742,20752,20762,20791,20817,20842,20848,20851,20865,20872,20876,20884,20919,21000,21016,21060,21083,21104,21111,21131,21167,21186,21206,21207,21212,21247,21261,21282,21298,21303,21318,21320,21333,21344,21354,21358,21360,21364,21366,21383,21405,21454,21468,21476,21514,21524,21525,21556,21566,21568,21576,21609,21621,21625,21644,21649,21655,21663,21674,21698,21702,21710,21742,21780,21784,21800,21803,21834,21842,21847,21868,21898,21902,21923,21948,21967,22029,22043,22045,22053,22055,22105,22109,22123,22124,22341,22692,22695,22739,22799,22846,22914,22986,22996,23040,23176,23354,23531,23557,23608,23679,23781,23965,23980,24007,24279,24511,24594,24606,24644,24854,24910,25003,25157,25240,25280,25337,25375,25462,25541,25546,25709,25931,26407,26415,26720,26872,26966,27015,27195,27444,27473,27482,27707,27892,27899,28122,28369,28465,28493,28543,28547,28641,28840,28973,29078,29243,29256,29810,29823,29977,30263,30303,30365,30544,30656,30697,30704,30718,30975,31059,31073,31109,31189,31195,31335,31337,31365,31625,31681,31731,31891,32345,32385,32528,32768,32769,32770,32771,32772,32773,32774,32775,32776,32777,32778,32779,32780,32798,32815,32818,32931,33030,33249,33281,33354,33355,33459,33717,33744,33866,33872,34038,34079,34125,34358,34422,34433,34555,34570,34577,34578,34579,34580,34758,34796,34855,34861,34862,34892,35438,35702,35777,35794,36108,36206,36384,36458,36489,36669,36778,36893,36945,37144,37212,37393,37444,37602,37761,37783,37813,37843,38037,38063,38293,38412,38498,38615,39213,39217,39632,39683,39714,39723,39888,40019,40116,40441,40539,40622,40708,40711,40724,40732,40805,40847,40866,40915,41058,41081,41308,41370,41446,41524,41638,41702,41774,41896,41967,41971,42056,42172,42313,42431,42434,42508,42557,42577,42627,42639,43094,43195,43370,43514,43686,43824,43967,44101,44160,44179,44185,44190,44253,44334,44508,44923,44946,44968,45247,45380,45441,45685,45722,45818,45928,46093,46532,46836,47624,47765,47772,47808,47915,47981,48078,48189,48255,48455,48489,48761,49152,49153,49154,49155,49156,49157,49158,49159,49160,49161,49162,49163,49165,49166,49167,49168,49169,49170,49171,49172,49173,49174,49175,49176,49177,49178,49179,49180,49181,49182,49184,49185,49186,49187,49188,49189,49190,49191,49192,49193,49194,49195,49196,49197,49198,49199,49200,49201,49202,49204,49205,49207,49208,49209,49210,49211,49212,49213,49214,49215,49216,49220,49222,49226,49259,49262,49306,49350,49360,49393,49396,49503,49640,49968,50099,50164,50497,50612,50708,50919,51255,51456,51554,51586,51690,51717,51905,51972,52144,52225,52503,53006,53037,53571,53589,53838,54094,54114,54281,54321,54711,54807,54925,55043,55544,55587,56141,57172,57409,57410,57813,57843,57958,57977,58002,58075,58178,58419,58631,58640,58797,59193,59207,59765,59846,60172,60381,60423,61024,61142,61319,61322,61370,61412,61481,61550,61685,61961,62154,62287,62575,62677,62699,62958,63420,63555,64080,64481,64513,64590,64727,65024]
        for port in ports:
            queue.put(port)
    elif mode == 4:
        custom_ports = input("Enter custom ports separated by space: ")
        ports = list(map(int, custom_ports.split()))
        for port in ports:
            queue.put(port)

def scan_port(protocol,port):
    try:
        sock = socket.socket(socket.AF_INET, protocol)
        sock.settimeout(1)
        result = sock.connect_ex((target, port))
        if result == 0:
            return True
        return False
    except Exception as e:
        return False

def worker(protocol):
    while not queue.empty():
        port = queue.get()
        if scan_port(protocol, port):
            print(f"{'➣'*5} Port {Fore.GREEN} {port} {Style.RESET_ALL} is open")
            open_ports.append(port)


def run_scanner(threads, mode, protocol):
    if protocol == socket.SOCK_STREAM:
        tcp_mode(mode)
    elif protocol == socket.SOCK_DGRAM:
        udp_mode(mode)
    else:
        print("Invalid choice !!!")
    thread_list = []
    for _ in range(threads):
        thread = threading.Thread(target=worker, args=(protocol,))
        thread_list.append(thread)

    for thread in thread_list:
        thread.start()

    for thread in thread_list:
        thread.join()

    print("\nOpen ports:", open_ports)

def banner_ip(banners, address, port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(10)  # Set a timeout of 10 seconds for the socket connection
    try:
        s.connect((address, port))
        if port == 80:
            print("\n" + Fore.GREEN + "[+] HTTP PROTOCOL Found" + Style.RESET_ALL + f" - IP: {address} | PORT: {port}\n")
            message = b"GET / HTTP/1.1\r\n\r\n"
            s.sendall(message)
        banner_data = s.recv(4096)
        if banner_data:
            banners.append([(address, port), banner_data.decode('utf-8')])
        else:
            print(Fore.YELLOW + f"[-] No response from IP: {address} | PORT: {port}" + Style.RESET_ALL+ "\n")
    except socket.timeout:
        print(Fore.YELLOW + f"[-] Connection timed out for IP: {address} | PORT: {port}" + Style.RESET_ALL + "\n")
    except socket.error as e:
        if e.errno == errno.ECONNREFUSED:
            pass
        else:
            print(Fore.RED + f"[-] Error connecting to IP: {address} | PORT: {port}" + Style.RESET_ALL)
    s.close()

print("Select a protocol:")
print("1. TCP")
print("2. UDP")
protocol_choice = int(input("Enter the protocol number (1 or 2): "))

if protocol_choice == 1:
    run_scanner(200, int(input("Select a mode: 1 for 1024, 2 for 10000, 3 for common ports, 69 for all ,4 for custom: ")), socket.SOCK_STREAM)
elif protocol_choice == 2:
    run_scanner(200, int(input("Select a mode: 1 for 1024, 2 for 10000, 3 for common ports, 4 for custom: ")), socket.SOCK_DGRAM)
else:
    print("Invalid protocol choice. Please select 1 or 2 for TCP or UDP.")

print(f"{'➣'*5} Port scan complete {'➣'*5}\n")
print(Fore.GREEN + f"{'➣'*5} Info for these ports (Note: This information is predefined and may not be accurate for all use cases):" + Style.RESET_ALL+"\n")

# Iterate through the list of ports
for port in open_ports:
    if port in port_info:
        info = port_info[port]
        print(f"🢂 {Fore.CYAN}Port: {port} | Service: {info['Service']} | Protocol: {info['Protocol']} | Description: {info['Description']}{Style.RESET_ALL}\n")
    else:
        print(f"{Fore.RED}Port {port} not found in the dictionary{Style.RESET_ALL}\n")
print(f"{'➣'*5} Attempting the banner grabbing now: {'➣'*5}\n")
banners = []
for port in open_ports:
    banner_ip(banners, target, port)
for banner in banners:
    print(Fore.CYAN + f"BANNER for IP: {banner[0][0]} | PORT: {banner[0][1]}" + Style.RESET_ALL)
    print(f"🏁  ->  \n {banner[1]}")
    print(f"         -------------------------------------------------------------------------------------------      \n")





```
