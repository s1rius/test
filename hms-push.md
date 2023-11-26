# Push

## Push-base.apk


### 初始化

- PushApplication

```Java
public class PushApplication extends KitApplication { 
	public void onCreate() {
		// 初始化

	}
}

```

xj.X 

```Java
public static void X(Context context) {
	aay.af("send broadcast to system push for hms token.");
	aaa.e(context, v(context, null));
}
```

```Java
private static Intent v(Context context, String str) {
	Intent Y = Y(context);
	Y.setAction("com.huawei.android.push.intent.REGISTER");
	Y.putExtra("subjectId", str);
	Y.putExtra("isMultiSender", !TextUtils.isEmpty(str));
	return Y;
}
```



```Java
private static boolean ah(Context context) {
	try {
		File file = new File("/system/framework/hwpush.jar");
		if (iy()) {
			aay.af("push jarFile is exist in cust");
		} else {
			if (!file.isFile() && !"HONOR".equals(Build.MANUFACTURER)) {
				aay.cL("push jarFile is not exist");
				if (aaw.a.EMUI_SDK_INT >= 8) {
					aay.cL("framework push not exist, use HMS pushservice");
					return false;
				} else if (!aaw.g("ro.config.push_enable", "CN".equals(aaw.cK("ro.product.locale.region")))) {
					aay.af("framework not support push");
					return false;
				} else {
					String P = aaw.P("ro.build.version.emui", "-1");
					aay.cL("displayEmuiVersion " + P);
					if (!TextUtils.isEmpty(P) && P.contains("3.0")) {
						aay.cL("emui is 3.0,and framework push not exist, need vote apk or sdk to support pushservice");
						return false;
					}
				}
			}
			aay.af("push jarFile is exist");
		}
		List<ResolveInfo> queryIntentServices = context.getPackageManager().queryIntentServices(new Intent().setClassName("android", iA()), 128);
		if (queryIntentServices != null && queryIntentServices.size() != 0) {
			aay.cL("framework push exist, use framework push first");
			return true;
		}
		aay.cL("framework push not exist, need vote apk or sdk to support pushservice");
		return false;
	} catch (Exception e) {
		aay.b("check FrameworkPush exist exception.", e);
		return false;
	}
}

```


ConnectPushCore.java

```Java
public static void connectPushCore() {
        int i = qk;
        int i2 = 3;
        if (i == 0) {
            i2 = 0;
        } else if (i != 1) {
            if (i == 2) {
                i2 = 5;
            } else if (i == 3 || i == 4) {
                i2 = 15;
            }
        }
        aay.cL("connect push core time is " + qk + ", after " + i2 + "s, connect to push core");
        if (abw.a(new vt(), i2 * 1000)) {
            return;
        }
        aay.ag("connect push core msg not in to the message queue.");
        aav.O("HMS_PUSH_CONNECT_PUSH_CORE", "6");
    }

```

HuaweiApiClient.java

```

```










```
public static Context getCoreBaseContext() {
	return CoreApplication.getCoreBaseContext();
}

public static Context getCoreAppContext() {
	return getCoreBaseContext().getApplicationContext();
}

```
