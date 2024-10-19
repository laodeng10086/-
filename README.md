// ==UserScript==
// @name         南宁理工学院校园网自动登录脚本
// @namespace
// @version      1.1
// @description  自动登录南宁理工学院校园网，支持多种浏览器
// @author       laodeng
// @match        
// @icon         
// @grant        
// @downloadURL  
// @updateURL    
// ==/UserScript==

// *************   在引号中输入你的信息   *************
var username = "*******"; // 学号
var password = "*******";   // 密码
var port = 1;              // 运营商，默认联通，校园网：-1  联通：1  电信：3

(function() {
    window.addEventListener('load', function() {
        // 确认页面加载完成，防止元素还未渲染
        if (document.readyState === "complete") {
            try {
                // 检查是否已经登录
                if (document.body.innerHTML.includes("用户已登录") || document.body.innerHTML.includes("Login Success")) {
                    alert.log("你已经登录，不需要重新登录");
                    return;
                }

                // 设置运营商
                var ispSelect = document.querySelector("[name='ISP_select']");
                if (ispSelect) {
                    ispSelect.value = port;
                } else {
                    alert.error("找不到运营商选择框");
                }

                // 填入用户名和密码
                $("input[name='R3']").val(1);  // 可能不必要的隐藏参数
                $("input[name='DDDDD']").val(username);
                $("input[name='upass']").val(password);

                // 模拟点击登录按钮
                var loginButton = $("input[name='0MKKey']");
                if (loginButton.length > 0) {
                    loginButton.click();
                    alert.log("尝试登录...");
                } else {
                    alert.error("找不到登录按钮");
                }

            } catch (e) {
                alert.error("脚本运行出错:", e);
            }
        } else {
            alert.warn("页面尚未完全加载，请稍等");
        }
    }, false);
})();
