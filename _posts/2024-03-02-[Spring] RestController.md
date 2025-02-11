---
title:  "[Spring] RestController"
categories: [Backend,Java]
tags:
  [
    Controller,
    RestController,
    java,
    spring
  ] 
image: "/assets/img/title/spring.png"
---

# @RestController
* @Controller + 해당 컨트롤러에 전부 @ResposeBody 가 적용
# @ResponseBody 
* String으로 응답시 View Template 사용 X
* return 값을 Http 바디에 담아서 그대로 보냄

# Spring에서의 Controller사용법
스프링에서의 컨트롤러를 지정해주기 위한 어노테이션은 `@Controller`와 `@RestController`가 있다.

* `@Controller`(Spring MVC Controller)
  * 전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환하기 위해 사용합니다.
  하지만 @ResponseBody 어노테이션과 같이 사용하면 RestController와 똑같은 기능을 수행할 수 있습니다.
  * 예시코드
    ```java
    @Controller
    public class Controllerprac {
        @GetMapping("/home") //home으로 Get요청이들어오면
        public String homepage(){
            return "home.html"; //home.html생성
        }
    }
    ```

* `@RestController`(Spring Restful Controller)Permalink
  * RestController는 Controller에서 @ResponseBody 어노테이션이 붙은 효과를 지니게 됩니다.
  * 즉 주용도는 JSON/XML형태로 객체 데이터 반환을 목적으로 합니다.
  * 예시코드
    ```java
    @RestController // JSON으로 데이터를 주고받음을 선언합니다.
    public class ProductRestController {

        private final ProductService productService;
        private final ProductRepository productRepository;

        // 등록된 전체 상품 목록 조회
        @GetMapping("/api/products")
        public List<Product> getProducts() {
            return productRepository.findAll();
        }
    }
    ```