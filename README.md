# CommandLineArchive<br>
通过终端命令行进行编译打包
## 命令行打包主要步骤<br>
1. 清理<br>
```
xcodebuild clean -workspace YourProjectName.xcworkspace -scheme YourProjectName -configuration Release
```
2. 编译<br>
```
xcodebuild -workspace YourProjectName.xcworkspace -scheme YourProjectName -archivePath build/YourProjectName.xcarchive archive
```
3. 打包<br>
```
xcodebuild -exportArchive -archivePath build/YourProjectName.xcarchive -exportPath build -exportOptionsPlist export.plist
```

## 其他注意事项<br>
#### 第三步打包需要有个export.plist文件才能打包成功<br>
export.plist文件代码如下：<br>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>compileBitcode</key>
	<false/>
	<key>method</key>
	<string>ad-hoc</string>
	<key>provisioningProfiles</key>
	<dict>
		<key>llqqb.borrowMoney</key>
		<string>yxbAdHoc</string>
	</dict>
	<key>signingCertificate</key>
	<string>iPhone Distribution</string>
	<key>signingStyle</key>
	<string>automatic</string>
	<key>stripSwiftSymbols</key>
	<true/>
	<key>teamID</key>
	<string>5J784PXPGS</string>
	<key>thinning</key>
	<string>&lt;none&gt;</string>
</dict>
</plist>
```

## export.plist需要你自己配置的信息：<br>
#### * method: 打的包的类型（app-store, ad-hoc, package, enterprise, development, and developer-id）<br>
#### * provisionProfiles: 项目的包名和对应ProvisionProfiles文件名<br>
#### * signingCertificate: 是否是开发环境还是生产环境<br>
#### * teamID: TeamID（通过AppleDeveloper查看）<br>

