# SmartCamera_Android
������ Android ƽ̨����������ͷ SDK��֧�� SmartLink �������������������֣�������ͷ���������á�����Ƶ�������ã��Լ� RTMP �������õȡ�
SmartCamera ּ���ṩ�����õ� SDK�����ݰ�������������ͷ���������ͷ�ȸ�������ͷ�豸��ʵ�ֶ�����ͷ��������õ����ܻ����ƶ�����

## ��ʶ SmartCamera
- SDK ����ṹ��
![Overview](overview.png)
- SmartCamera��SmartCamera ��һ������ʵ������ʹ�� SDK �������
- CameraProvider��CameraProvider ��һ���ӿڣ���Բ�ͬ���̵�����ͷ���ṩ��ͬ�� CameraProvider ʵ��
- Camera��Camera ͬ����һ���ӿڣ���Բ�ͬ�����ṩ��Ӧ��ʵ��

## ʹ�� SmartCamera
- ���ز����� smartcamera-x.x.x.jar��ͬʱ���� okHttp ��ص� jar �ļ������̡�
- �������룺
```java
final SmartCamera g = SmartCamera.getInstance();

// SmartLink ��������
g.smartlink("APName", "APPassword", 10);

// ����������
g.discover(g.getSupported(), new CameraDiscoveryConsumer(){

    @Override
    public void cameraDiscoverAbort(CameraProviderSource source) {
        System.out.println(String.format("ABORT: %s", source.getName()));
    }

    @Override
    public void cameraDiscoverTimeout(CameraProviderSource source) {
        System.out.println(String.format("TIMEOUT: %s", source.getName()));
    }

    @Override
    public void cameraDiscovered(CameraSource source) {
        System.out.println(String.format("FOUND: %s, %s", source.getName(), source.getUrl()));
        
        // ��������ͷ
        Camera camera = g.connect(source.getUrl());

        if(camera != null) {
            System.out.println(String.format("NAME: %s", camera.getName()));
            
            // ��ȡ����ͷ������Ϣ
            NetworkConfig netconf = camera.getNetwork();
        
            if(netconf != null)
                System.out.println(String.format("MAC: %s, DHCP: %s, IP: %s, MASK: %s, GATEWAY: %s, DNS1: %s, DNS2: %s",
                    netconf.macAddr, netconf.dhcp ? "yes" : "no", netconf.ip, netconf.mask, netconf.gateway, netconf.dns1, netconf.dns2));

            // ��ȡ����ͷ WiFi ������Ϣ
            WiFiConfig wificonf = camera.getWiFi();

            if(wificonf != null)
                System.out.println(String.format("ENABLED: %s, SSID: %s, PWD: %s",
                    wificonf.enabled ? "yes" : "no", wificonf.ssid, wificonf.password));

            // ��ȡ��Ƶ����
            AudioConfig audioconf = camera.getAudio();
            
            if(audioconf != null)
                System.out.println(String.format("ENABLED: %s, CODEC: %d, SAMPLE: %d, BITRATE: %d, VOLUME: %d",
                    audioconf.enabled ? "yes" : "no", audioconf.codec, audioconf.samplerate, audioconf.bitrate, audioconf.volume));

            // ��ȡ��Ƶ����
            VideoConfig videoconf = camera.getVideo();
            
            if(videoconf != null)
                System.out.println(String.format("ENABLED: %s, CODEC: %d, RESO: %d, BRCTRL: %d, BITRATE: %d, FPS: %d",
                    videoconf.enabled ? "yes" : "no", videoconf.codec, videoconf.reso, videoconf.brctrl, videoconf.bitrate, videoconf.framerate));

            // ��ȡ����ͷ RTMP ������Ϣ
            RtmpConfig rtmpconf = camera.getRtmp();
            
            if(rtmpconf != null)
                System.out.println(String.format("ENABLED: %s, RTMP: %s, USER: %s, PWD: %s",
                    rtmpconf.enabled() ? "yes" : "no", rtmpconf.rtmpUrl, rtmpconf.user, rtmpconf.password));
            
            // ��ȡ����ͷ RTSP ���ŵ�ַ
            RtspConfig rtspconf = camera.getRtsp();
            
            if(rtspconf != null)
                System.out.println(String.format("MAIN: %s, SUB: %s", rtspconf.mainUrl, rtspconf.subUrl));

            if("192.168.1.199".equals(source.getName())) {
                // ��������ͷ����
                camera.setName("SmartCamera199");
                
                netconf = new NetworkConfig();
                
                netconf.dhcp = false;
                netconf.ip = "192.168.1.198";
                
                // ��������ͷ����
                camera.setNetwork(netconf);
                
                wificonf = new WiFiConfig();

                // ��������ͷ WiFi ������Ϣ
                camera.setWiFi(wificonf);
                
                audioconf = new AudioConfig();
                
                audioconf.enabled = false;
                audioconf.volume = 90;

                // ������Ƶ����
                camera.setAudio(audioconf);

                videoconf = new VideoConfig();

                videoconf.reso = VideoConfig.RESO_1080P;
                videoconf.bitrate = 850;
                videoconf.brctrl = VideoConfig.CTRL_CBR;

                // ������Ƶ����
                camera.setVideo(videoconf);

                // RTMP ��������
                rtmpconf = new RtmpConfig();

                // ���� RTMP ����
                camera.setRtmp(rtmpconf);
            }

            // �ָ���������
            // camera.restore();

            // �Ͽ�����
            camera.disconnect();
        }
    }
    
}, 5);
```


## ���������
���������κ�����ʱ������ͨ���� GitHub �� repo �ύ issues ���������⣬�뾡���ܵ�����������������⣬����д�����ϢҲһͬ������������ Labels ��ָ������Ϊ bug ����������
[ͨ������鿴���е� issues ���ύ Bug](https://github.com/azhisoft/SmartCamera_Android/issues)
