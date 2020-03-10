---
title: "안드로이드 스튜디오 애드몹 광고 관리하기 / TestDevice / 깃허브 광고아이디 숨기기 / 무효 트래픽 정지 "
date: 2020-03-10
categories: 
  - 안드로이드
tags: 
  - 안드로이드
  - android studio
  - admob
  - 애드몹
---

# 효율적으로 애드몹 광고 관리하기 

```
public class IDManger {
    static boolean isTest = true;
    
    static String myBannerId = "Your ID ";
    static String testBannerId = "ca-app-pub-3940256099942544/6300978111";
    static String myPopupId = " Your ID ";
    static String testPopupId = "ca-app-pub-3940256099942544/1033173712";
    
    static AdRequest adRequest = new AdRequest.Builder().
            addTestDevice("XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX").
            addTestDevice("YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY").
            build();
            
    public static void SetBannerAd(Context context, FrameLayout av) {
        MobileAds.initialize(context, new OnInitializationCompleteListener() {
            @Override
            public void onInitializationComplete(InitializationStatus initializationStatus) {
            }
        });
        AdView mAdView = new AdView(context);
        mAdView.setAdSize(new AdSize(300, 50));
        if(!isTest)
            mAdView.setAdUnitId(myBannerId);
        else
            mAdView.setAdUnitId(testBannerId);
        FrameLayout frameLayout = av;
        frameLayout.addView(mAdView);

        mAdView.loadAd(adRequest);
    }

    public static InterstitialAd SetPopUpAd(Context context) {
        MobileAds.initialize(context, new OnInitializationCompleteListener() {
            @Override
            public void onInitializationComplete(InitializationStatus initializationStatus) {
            }
        });
        InterstitialAd popupAd = new InterstitialAd(context);
        if(!isTest)
            popupAd.setAdUnitId(myPopupId);
        else
            popupAd.setAdUnitId(testPopupId);
        popupAd.loadAd(adRequest);
        return popupAd;
    }
}
```

그대로 복사해서 만들고 사용 하면 끝 

## isTest
```
static boolean isTest = true;
```
이 부분을 수정하면 된다. 테스트 하는 도중이라면 true로 놔두고, 릴리즈 할 때에 false 로 바꿔주고 릴리즈 하면 끝난다. 

## ad id 
```
    static String myBannerId = "Your Banner ID ";
    static String testBannerId = "ca-app-pub-3940256099942544/6300978111";
    static String myPopupId = " Your Popup ID ";
    static String testPopupId = "ca-app-pub-3940256099942544/1033173712";
```
여기서 배너와 팝업 광고 id 를 " Your ID " 부분에 채워 주면 된다. 


# Test Device (테스트 기기란)?

테스트 기기란, 말 그대로 테스트 기기이니, 광고비를 지불 하지 않아도 된다!

라고 광고주에게 알리는 기능 입니다. 

즉 테스트기기를 등록 해 주면, 무효 트래픽으로 걸릴 걱정 없이 테스트 해 볼 수 있다. 

다만, 테스트 기기를 사용함에도 불구하고 무효 트래픽으로 애드몹 계정이 정지 가능성이 

있다고 하니, 위의 isTest 를 수정해 가며 사용 하는 것이 안전하다. 

테스트 기기를 만드는데 성공한다면

![testad](https://user-images.githubusercontent.com/36880919/76312574-b11b2d00-6316-11ea-8f7f-27455962269b.png)

위와 같이 실제 광고 위에 test ad 라고 이름표가 붙게 된다. 

# Test Device 테스트기기 등록 방법

테스트 기기로 등록하고자 하는 기기로 어플을 실행하게 되면, 

로그에서 해당 사항을 볼 수 있다. 
```
I/Ads: Use AdRequest.Builder.addTestDevice("33BE2250B43518CCDA7DE426D04EE231")
to get test ads on this device."
```
여기서 addTestDevice("33BE2250B43518CCDA7DE426D04EE231") 이 부분을 그대로 복사 해 오면 된다. 

그리고 다시 위의 본문에서 
```
    static AdRequest adRequest = new AdRequest.Builder().
            addTestDevice("XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX").
            addTestDevice("YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY").
            build();
```
여기서 XXXX, YYYY 부분을 위에서 확인한 기기 이름을 넣어 주면 된다. 

그 후 다시 해당 기기에서 실행을 하게 되면

```
I/Ads: This request is sent from a test device.
```
이제는 위와 같이, test device 에서 실행 했다는 로그를 확인 할 수 있다. 

근데, 직접 연결해서 기기를 볼 수 있으면 좋지만, 

같이 팀 프로젝트를 한다거나, 멀리 있는 사람의 디바이스 아이디를 확인 해야 한다?

아니면 테스트 디바이스 아이디가 혹시 변경됬는지 자주 확인을 하려면? 

(안드로이드 버전 업데이트 하면 디바이스 아이디가 바뀔 수 있다고 한다. )

https://play.google.com/store/apps/details?id=com.sanha.getdeviceid

위 링크의 어플을 다운받거나, 다운받을것을 부탁해서 

디바이스 아이디를 받아 오는 방법 도 있다. 

위 어플리케이션 말고도, 디바이스 아이디를 찾아 주는 어플은 많으니, 검색 해서 받아도 무방하다. 


# 무효 트래픽 제한 후기 
 위 사항을 제대로 지키지 못해 무효 트래픽으로 인한 애드몹 임시 정지 ( 제한 ) 을 당한 적이 있다...
 
 광고가 하나도 안뜬다. 
 
 너무 귀찮아서, 또 급하게 업데이트 할 게 있어서 딱 하루 안지켰더니 정지 당했다... 
 
 그래서 편하게 관리를 위해 위와 같이 따로 클래스를 만들어서 사용 하고 있다. 
 
 제한을 당하고 22일이 지나서야 풀렸다. 
 
 이의 제기도 불가능 하니 미리미리 애드몹 정책에 위반 되지 않도록 조심하자. 
 
 나 이외에도 많은 사람들이 선례로 기다리는거 외에는 답이 없다. 
 
 10일~ 30일 랜덤하게 기다려야 풀린 다고 한다. 
 
 ( 참고로, 경고 누적 등의 이유로 아에 정지를 당하면, 이의 제기를 신청 할 수 있다고 한다. )
 
 
