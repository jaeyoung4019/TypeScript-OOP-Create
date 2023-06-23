# 객체생성을 통해 객체지향의 법칙을 지키면서 JavaScript 를 구상할 수 있습니다.

예를 들어, 빌더 패턴을 활용해 API 에 대한 객체를 생성해 매개변수로 활용하는 예시를 보면

필요한 Parameter -> url , mutipart-used , param

```ts
/**
 * API 요청시 보낼 객체를 생성하는 클래스
 */
export class APIConfig {
    public url: string;
    public param: paramInterface | null;
    public multipartUse: boolean;

    private constructor(
        url: string,
        param: paramInterface | null,
        multipartUse: boolean
    ) {
        this.param = param;
        this.url = url;
        this.multipartUse = multipartUse;
    }

    static Builder = class {
        private _url = '';
        private _param = null;
        private _multipartUse = false;

        setUrl(value: string) {
            this._url = value;
            return this;
        }

        setParam(value: any) {
            this._param = value;
            return this;
        }

        setMultipartUse(value: boolean) {
            this._multipartUse = value;
            return this;
        }

        build() {
            return new APIConfig(this._url, this._param, this._multipartUse);
        }
    };
}

```

이런 형식으로 짜게 된다면 Spring 의 lombok @Build 처럼
빌더 패턴을 활용해서 객체를 생성하여 매개변수로 활용할 수 있습니다. 
이렇게 되면 API Parameter 라는 기능을 담당하는 클래스를 하나 생성하여 따로 뺄 수 있다는 장점이 생깁니다. 
그럼 API 를 요청할 때 좀 더 모듈화 하여 처리할 수 있죠. 
