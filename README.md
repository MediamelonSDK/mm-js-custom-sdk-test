# MediaMelon Custom JS SDK Integration Guide

## Step 1: Add MediaMelon Player SDK via NPM

## Step 2: Register and Initialize MediaMelon Player SDK

> **Note**: CUSTOMER_ID is your MediaMelon assigned Customer ID. If you do not know your Customer ID, contact MediaMelon at customer-support@mediamelon.com.

### Step 2.1: Instantiate and Register SDK

```javascript
var mmJSPlugin = new mmJSCustomAdapter();
mmJSPlugin.registerMMSmartStreaming(
    "PLAYER_NAME", 
    "CUSTOMER_ID", 
    "SUBSCRIBER_ID", 
    "DOMAIN_NAME", 
    "SUBSCRIBER_TYPE", 
    "SUBSCRIBER_TAG", 
    hash_subscriber_id      // Boolean Value
);
```

> **Note**: `hash_subscriber_id`: Set it to true to hash the subscriber ID, and to false to process the subscriber ID without hashing.

### Step 2.2: Report Player Information

```javascript
mmJSPlugin.reportPlayerInfo("PLAYER_BRAND", "PLAYER_MODEL", "PLAYER_VERSION");            
mmJSPlugin.reportBasePlayerInfo("BASE_PLAYER_NAME", "BASE_PLAYER_VERSION");
```

### Step 2.3: Report Application Information

```javascript
mmJSPlugin.reportAppInfo("APPLICATION_NAME", "APPLICATION_VERSION");
```

### Step 2.4: Report Device Information

```javascript
var deviceInfo = {
    "deviceName": "DEVICE_NAME",
    "deviceBrand": "DEVICE_BRAND",
    "deviceModel": "DEVICE_MODEL",
    "deviceId": "DEVICE_ID",
    "deviceOS": "DEVICE_OS",
    "deviceOSVersion": "DEVICE_OS_VERSION",            
    "screenWidth": screen_width,        // Integer Value
    "screenHeight": screen_height       // Integer Value
};
mmJSPlugin.reportDeviceInfo(deviceInfo);
```

### Step 2.5: Report Experiment Name & Sub Property ID

```javascript
mmJSPlugin.reportExperimentName("EXPERIMENT_NAME");
mmJSPlugin.reportSubPropertyId("SUB_PROPERTY_ID");
```

### Step 2.6: Initialize Session with Content Metadata

```javascript
var contentMetaData = {
    "assetName": "ASSET_NAME",
    "assetId": "ASSET_ID",
    "videoId": "VIDEO_ID",
    "contentType": "CONTENT_TYPE",
    "genre": "GENRE",
    "drmProtection": "DRM_PROTECTION",
    "episodeNumber": "EPISODE_NUMBER",
    "season": "SEASON",
    "seriesTitle": "SERIES_TITLE",
    "videoType": "VIDEO_TYPE"
};

mmJSPlugin.initializeSession(contentMetaData, "STREAM_URL");
mmJSPlugin.reportUserInitiatedPlayback();
```

### Step 2.7: Report View Session ID

```javascript
mmJSPlugin.reportViewSessionId("VIEW_SESSION_ID");
```

## Step 3: Custom Metadata

> **Note**: Check the custom tags configuration in your dashboard and report accordingly. If the custom tags are not configured, please configure and use them accordingly.

```javascript
mmJSPlugin.reportCustomMetadata("custom_1", "value1");
mmJSPlugin.reportCustomMetadata("custom_2", "value2");
```

## Step 4: Stream and Network Information

### Step 4.1: Report Stream Information

```javascript
var streamInfo = {
    "streamURL": "NEW_STREAM_URL",
    "streamFormat": "STREAM_FORMAT",
    "mediaType": "MEDIA_TYPE",
    "sourceType": "SOURCE_TYPE",
    "duration": video_duration,  // Integer Value in Milli Seconds
    "isLive": is_live           // Boolean Value
}
mmJSPlugin.reportStreamInfo(streamInfo);
```

> **Note**: `is_live`: Set isVideoLive to true for live video stream and to false for the VOD stream

### Step 4.2: Update DRM Type

```javascript
mmJSPlugin.updateDRMType("NEW_DRM_TYPE");
```

### Step 4.3: Report Network Information

```javascript
var networkInfo = {
    "cdn": "CDN",
    "asn": asn,                 // Integer Value
    "hostName": "SOURCE_HOST_NAME",
    "networkType": "NETWORK_TYPE",
    "networkOperator": "NETWORK_OPERATOR"
}
mmJSPlugin.reportNetworkInfo(networkInfo);
```

## Step 5: Player Events

### Step 5.1: Report Player State

```javascript
mmJSPlugin.reportPlayerState(MMPlayerState.PLAYING);
```

**Enum: MMPlayerState**
- PLAYING
- PAUSED
- STOPPED

### Step 5.2: Report Buffering

```javascript
mmJSPlugin.reportBufferingStarted();
mmJSPlugin.reportBufferingCompleted();
```

### Step 5.3: Report Seek

```javascript
mmJSPlugin.reportPlayerSeekStarted();
mmJSPlugin.reportPlayerSeekCompleted();
```

### Step 5.4: Report Error

```javascript
mmJSPlugin.reportError("ERROR_CODE", "ERROR_MESSAGE", "ERROR_DETAILS");
```

### Step 5.5: Report Playback Position

> **Note**: Call this every 0.5 sec or 1 sec to report the playback position from the player

```javascript
mmJSPlugin.reportPlaybackPosition(playback_position); // Integer Value in Milli Seconds
```

## Step 6: Manifest & Chunk Request Status

### Step 6.1: Report Fallback Event

```javascript
mmJSPlugin.reportFallbackEvent("FALLBACK_MANIFEST_URL", "DESCRIPTION");
```

### Step 6.2: Report Manifest Request Status

```javascript
mmJSPlugin.reportManifestRequestStatus(ManifestRequestStatus.FAILED, "DESCRIPTION");
```

**Enum: ManifestRequestStatus**
- FAILED
- CANCELLED

### Step 6.3: Report Chunk Request Status

```javascript
mmJSPlugin.reportChunkRequestStatus(ChunkRequestStatus.FAILED, ChunkType.VIDEO, {"KEY": "VALUE"});
```

**Enum: ChunkRequestStatus**
- FAILED
- CANCELLED

**Enum: ChunkType**
- VIDEO
- AUDIO

## Step 7: Ad Data & Ad Events

### Step 7.1: Report Ad Break Start & End

```javascript
mmJSPlugin.reportAdBreakStart();
mmJSPlugin.reportAdBreakEnd();
```

### Step 7.2: Report Ad Data, Ad Start & End

```javascript
var adInfo = {
    "adTitle": "AD_TITLE",
    "adId": "AD_ID",
    "adCreativeId": "AD_CREATIVE_ID",
    "adCreativeType": "AD_CREATIVE_TYPE",
    "adClient": "AD_CLIENT",
    "adPosition": "AD_POSITION",               // pre, mid, post
    "adServer": "AD_SERVER",
    "adResolution": "AD_RESOLUTION",
    "adUrl": "AD_URL",
    "adDuration": ad_duration,              // Double Value
    "adPodIndex": pod_index,                // Integer Value
    "adPositionInPod": ad_position_in_pod,  // Integer Value
    "isBumper": is_bumper                   // Boolean Value
}

mmJSPlugin.reportAdStart(adInfo);
mmJSPlugin.reportAdEnd();