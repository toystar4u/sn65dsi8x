# sn65dsi8x
MIPI-DSI to LVDS Bridge Driver for TI SN65DSI83/84/85


## Kernel Configuration


## LVDS Display
Display Timings for Hannstar HSD070pww1 


## Devicetree

- I2C address: 0x2d
- imx8mq SoC : DCSS with MIPI-DSI 

```
&i2c1 {
	
	dsi85:dsi85@2d {
		compatible = "ti,sn65dsi83";
		reg = <0x2d>;
		ti,dsi-lanes = <4>;

		// format 2(0) must be selected when RGB666(18bpp) data is received from DSI
		// format 1(1) must be selected when RGB888(24bpp) data is received from DSI 
		//	while 18bpp panel(LVDS) is selected 

		// "ti,sn65dsi83" driver only support RGB888 for DSI 
		ti,lvds-bpp = <18>;
		ti,lvds-format = <1>;		
		ti,width-mm = <151>;
		ti,height-mm = <94>;
		ti,test-mode = <0>;       	// enable test mode

		enable-gpios = <&gpio1 6 GPIO_ACTIVE_HIGH>;
		pinctrl-names = "default";
		pinctrl-0 = <&pinctrl_mipi_dsi_en>;
		status = "okay";
	
		display-timings {
			native-mode = <&lvds_timing0>;
			lvds_timing0:hsd070pww1 {	
				clock-frequency = <8500000>;  // 82MHz in product mannual
        hactive = <1280>;
        vactive = <800>;
        hfront-porch = <10>;
        hback-porch = <10>;
        hsync-len = <661>;
        vback-porch = <10>;
        vfront-porch = <10>;
        vsync-len = <203>;
        hsync-active = <0>;
				vsync-active = <0>;
				de-active = <1>;
				pixelclk-active = <0>;
			};

		};

		port{
			dsi85_in: endpoint {
				remote-endpoint = <&mipi_bridge_out>;
			};
		};

	};

};
```
