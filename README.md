Project的build.gradle加入这句
maven {url "https://raw.githubusercontent.com/ALSYLY/avatarmobi/master"}
依赖加入：
implementation 'com.alsy.ads:Jelly:1.0.2'

Sdk初始化：
SmartAds.init(activity, appid, subid, debugMode);
activity:当前的Activity
appid(String):
subid(String):
debugMode(boolean):是否为debug模式
此操作仅需执行一次，最好是在应用启动时执行。
覆盖您活动的生命周期方法。
@Override protected void onStart() { super.onStart(); SmartAds.onStart(this); } @Override	protected	void	onResume(){super.onResume(); SmartAds.onResume(this); } 
@Override protected void onStop() { super.onStop(); SmartAds.onStop(this); } @Override protected void onPause() {super.onPause(); SmartAds.onPause(this); } 
@Override protected void onDestroy() {super.onDestroy(); SmartAds.onDestroy(this); } 
@Override public void onBackPressed() { super.onBackPressed(); SmartAds.onBackPressed(this); }

广告分三种
1.横幅
OADBanner oadBanner = new OADBanner(activity); 
ViewGroup container = findViewById(R.id.container);
oadBanner.LoadBanner(container); 
事件监听（可选）
oadBanner.setAdBannerListener(new ADBannerListener() { 
@Override public void onAdLeftApplication(String var1) { } 
@Override public void onBannerLoaded(String var1, View var2) { } 
@Override public void onBannerUnloaded(String var1) { } 
@Override public void onBannerShow(String var1) { }
 @Override public void onBannerClick(String var1) { } 
@Override public void onBannerHide(String var1) { }
 @Override public void onBannerError(String var1) { }
 @Override public void onBannerClosed(String var1) { } });
container: 广告容器
activity:为当前界面

2.插屏
OADInterstitial oadInterstitial = new OADInterstitial(activity);创建
oadInterstitial.LoadInterstitial();加载广告
if (oadInterstitial .isLoaded()) 
 oadInterstitial .show();//显示广告前要判断广告是否加载完成才展示。
应该事先对广告进行加载，不可以调用LoadInterstitial(）后，马上调用show()方法。
事件监听（可选）
oadInterstitial.setAdInterstitialListener(new ADInterstitialListener() { 
@Override public void onAdClosed() { } 
@Override public void onAdFailedToLoad(int var1) { } 
@Override public void onAdLeftApplication() { } 
@Override public void onAdOpened() { } 
@Override public void onAdLoaded() { } 
@Override public void onAdClicked() { } 
@Override public void onAdImpression() { } });
3.激励广告
OADVideo oadVideo = new OADVideo(activity);
oadVideo.loadVideo();
if (oadVideo.isLoaded()) 
 oadVideo.show( );
事件监听（可选）
oadVideo.setRewardedVideoAdListener(new ADRewardedVideoListener() { 
@Override public void onRewardedVideoAdLoaded() { } 
@Override public void onRewardedVideoAdOpened() { } 
@Override public void onRewardedVideoStarted() { } 
@Override public void onRewardedVideoAdClosed() { }
 @Override public void onRewarded(ADRewardItem var1) { } 
@Override public void onRewardedVideoAdLeftApplication() { }
 @Override public void onRewardedVideoAdFailedToLoad(int var1) { }
 @Override public void onRewardedVideoCompleted() { } });