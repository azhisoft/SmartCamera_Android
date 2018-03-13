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
					netconf.getMacAddr(), netconf.isDHCPEnabled() ? "yes" : "no", netconf.getIP(), netconf.getMask(), netconf.getGateway(), netconf.getDNS1(), netconf.getDNS2()));

			// ��ȡ����ͷ WiFi ������Ϣ
			WiFiConfig wificonf = camera.getWiFi();

			if(wificonf != null)
				System.out.println(String.format("ENABLED: %s, SSID: %s, PWD: %s",
					wificonf.isEnabled() ? "yes" : "no", wificonf.getSSID(), wificonf.getPassword()));

			// ��ȡ��Ƶ����
			AudioConfig audioconf = camera.getAudio();
			
			if(audioconf != null)
				System.out.println(String.format("ENABLED: %s, CODEC: %d, SAMPLE: %d, BITRATE: %d, VOLUME: %d",
					audioconf.isEnabled() ? "yes" : "no", audioconf.getCodec(), audioconf.getSamplerate(), audioconf.getBitrate(), audioconf.getVolume()));

			// ��ȡ��Ƶ����
			VideoConfig videoconf = camera.getVideo();
			
			if(videoconf != null)
				System.out.println(String.format("ENABLED: %s, CODEC: %d, RESO: %d, BRCTRL: %d, BITRATE: %d, FPS: %d",
					videoconf.isEnabled() ? "yes" : "no", videoconf.getCodec(), videoconf.getReso(), videoconf.getBrctrl(), videoconf.getBitrate(), videoconf.getFramerate()));

			// ��ȡ����ͷ RTMP ������Ϣ
			RtmpConfig rtmpconf = camera.getRtmp();
			
			if(rtmpconf != null)
				System.out.println(String.format("ENABLED: %s, RTMP: %s, USER: %s, PWD: %s",
					rtmpconf.isEnabled() ? "yes" : "no", rtmpconf.getRtmpUrl(), rtmpconf.getUser(), rtmpconf.getPassword()));
			
			// ��ȡ����ͷ RTSP ���ŵ�ַ
			RtspConfig rtspconf = camera.getRtsp();
			
			if(rtspconf != null)
				System.out.println(String.format("MAIN: %s, SUB: %s", rtspconf.getMainUrl(), rtspconf.getSubUrl()));

			if("192.168.1.199".equals(source.getName())) {
				// ��������ͷ����
				camera.setName("SmartCamera199");
				
				netconf = new NetworkConfig();
				
				netconf.setDHCPEnabled(false);
				netconf.setIP("192.168.1.198");
				
				// ��������ͷ����
				camera.setNetwork(netconf);
				
				wificonf = new WiFiConfig();

				// ��������ͷ WiFi ������Ϣ
				camera.setWiFi(wificonf);
				
				audioconf = new AudioConfig();
				
				audioconf.setEnabled(false);
				audioconf.setVolume(90);

				// ������Ƶ����
				camera.setAudio(audioconf);

				videoconf = new VideoConfig();

				videoconf.setReso(VideoConfig.RESO_1080P);
				videoconf.setBitrate(850);
				videoconf.setBrctrl(VideoConfig.CTRL_CBR);

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
