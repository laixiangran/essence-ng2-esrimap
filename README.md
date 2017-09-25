# essence-ng2-esrimap

essence-ng2-esrimap is a esrimap component for Angular.

## Usage

1. Install

	```shell
	npm install --save essence-ng2-esrimap@latest
	```

2. Set in the .angular-cli.json（@angular/cli）

	```json
    "styles": [
        "../node_modules/font-awesome/css/font-awesome.min.css"
    ]
	```

3. Add the EssenceNg2EsriMapModule

	```typescript
	import {EssenceNg2EsriMapModule} from "essence-ng2-esrimap";
	@NgModule({
	    imports: [
	        EssenceNg2EsriMapModule
	    ]
	})
	```

4. Use in the template

	```html
    <essence-ng2-esrimap
            [gisApiUrl]="gisApiUrl"
            [geoUrl]="geoUrl"
            [mapUrl]="mapUrl"
            [esriCSSUrl]="esriCSSUrl"
            (mapReady)="onMapReady($event)"
            (exentChange)="onExentChange($event)">
    </essence-ng2-esrimap>
	```

5. Use in the component

	```typescript
    esriMap: EssenceNg2EsriMapComponent;
    mapUrl: string = 'http://192.168.0.109:8399/arcgis/rest/services/HD_BASEMAP/MapServer';
    geoUrl: string = 'http://192.168.0.109:8399/arcgis/rest/services/Geometry/GeometryServer';
    gisApiUrl: string = 'http://192.168.0.109/arcgis_api/3.14/init.js';
    esriCSSUrl: string = 'http://192.168.0.8/arcgis_api/3.14/esri/css/esri.css'; // esri.css路径

    onMapReady($event: EssenceNg2EsriMapComponent) {
        this.esriMap = $event;
    }

    onExentChange(event: any) {
        console.log(event);
    }
	```

### 注意

如果出现跨域的问题，请检查项目根目录下是否存在`proxy.config`及`proxy.jsp`，没有请放置。

## API

### Inputs

- `isProxy`（`boolean?=false`） - 是否开启代理

- `mapUrl`（`string[] | string`） - 基础底图路径

- `mapType`（`string?='esri'`） - 基础底图类型，`tdt`：天地图，`esri`：esri地图服务

- `geoUrl`（`string?='http://tasks.arcgisonline.com/ArcGIS/rest/services/Geometry/GeometryServer'`） - 几何服务路径，默认是在线路径，最好配置自己的路径

- `geoUrl`（`string?='http://tasks.arcgisonline.com/ArcGIS/rest/services/Geometry/GeometryServer'`） - 几何服务路径，默认是在线路径，最好配置自己的路径

- `esriCSSUrl`（`string?='http://js.arcgis.com/3.14/esri/css/esri.css'`） - esri.css路径，默认是在线路径，最好配置自己的路径

- `initExtent`（`Object`） - 初始地图范围，`{xmax, xmin, ymax, ymin}`

### Outputs

- `mapReady`：地图初始化完成后会触发该事件，参数$event为当前component实例对象

- `exentChange`：地图范围改变触发该事件，参数$event为当前地图范围对象

### Properties

- `map`（`any`） - 当前地图对象

### Instance Methods

- `loadEsriModules(modules: string[]): Promise<any>` - 加载ArcGIS API for JavaScript的模块，如：`['esri/map']`

- `gpAsyncGetResultData(params: AsyncGetResultParam): void` - GP服务获取数据（异步）

- `locationPoint(point: {x: number, y: number}): void` - 点定位

- `clearLocationLayer(): void` - 清除定位图层

- `showMapInfoWindow(params: any): void` - 显示地图信息窗口
         * params属性如下：
         * title {String} 信息窗口标题
         * content {String} 信息窗口内容，支持html
         * location {Point} 信息窗口位置
         * placement {String} 信息窗口方位
         * width {Number} 信息窗口宽度
         * height {Number} 信息窗口高度

- `hideMapInfoWindow(): void` - 隐藏地图信息窗口

- `exactProject(fs: any, wkid: any): Observable<any>` - 要素坐标转换

- `latToDec(dfm: string): number` - 将坐标由度分秒表示转为十进制表示

- `decToLat(sjz: number): string` - 将坐标由十进制表示转为度分秒表示

## Develop

	```shell
	npm install // 安装依赖包
	
	npm start // 启动项目
	```

# License

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](/LICENSE)
