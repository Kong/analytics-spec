# Standalone Proxy

**To support HTTPS or change any default options view the full [HARchiver README](https://github.com/APIAnalytics/HARchiver) on GitHub.**

**API creators can use the [reverse proxy option](https://github.com/APIAnalytics/HARchiver/blob/master/README.md#for-api-providers).**

1. Install HARchiver on your linux server, or [use docker](https://github.com/APIAnalytics/HARchiver#docker). 

    ``` shell
    wget https://github.com/Mashape/harchiver/releases/download/v1.3.1/harchiver.tar.gz
    tar xzvf harchiver.tar.gz
    cd release
    ```

2. Start HARchiver on port 15000 with your API analytics service token:

    ``` shell
    ./harchiver 15000 SERVICE-TOKEN
    ```

3. Now you can send requests through HARchiver using the `Host` header:

    ``` shell
    curl -H "Host: httpconsole.com" http://127.0.0.1:15000/ip
    ```

That's it, your data is now available on [apianalytics.com](http://www.apianalytics.com)! 
