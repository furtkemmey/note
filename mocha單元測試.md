# mocha 單元測試
## 安裝項目
- mocha
- chai // 斷言
- supertest // 模擬 HTTP Request 的套件

## package.json的scripts
在package.json加入之後可以用npm run test呼叫

    "test": "mocha --exit"

## app.js 輸出給test.js用
    module.exports = app;
    
## require()
    const app = require('../app.js'); // app 要 export
    const should = require('chai').should(); // should斷言
    const request = require('supertest')(app); // 模擬 HTTP Request 的套件
    
## 語法
    describe('API products 測試', function() { // 測試標題
          before(function() {
            // run before all tests in this block
          });
        
          after(function() {
            // run after all tests in this block
          });
        
          beforeEach(function() {
            // run before each test in this block
          });
        
          afterEach(function() {
            // run after each test in this block
          });
          
          it('連線根目錄', function(done) { // 測試內容標題
              request.get('/')            
                  .expect(200)
                  .end(function(err, res){
                      should.not.exist(err);
                      should.exist(res);
                      done()
                  });
          });
     });
## should斷言
    should.not.exist(err); // 沒有err
    should.exist(res);  // 有資料
    
    foo.should.be.a('string');
    res.body.should.be.an('object'); // 內容是物件
    
    res.body.should.have.property('status'); // 檢查屬性
    
    res.body.data.should.equal('haha'); // 檢查內容
    
    foo.should.have.lengthOf(3);
    
    beverages.should.have.property('tea').with.lengthOf(3);
    
# supertest 模擬 HTTP Request 的套件

## 引用
    const request = require('supertest')(app);
    
## get 範例
      it('測試 GET /products/ 回傳json,檢查屬性', function(done) {
          request.get('/products/')   
              .set('Accept', 'application/json') // 檢查 回傳格式為 JSON
              .expect('Content-Type', /json/) 
              .expect(200) // 檢查  回傳 HTTP 狀態碼為 200
              .end(function(err, res){
                  if (err) return done(err);
                  should.not.exist(err); // 沒有err
                  should.exist(res);  // 有資料
                  res.body.should.be.an('object'); // 內容是物件
                  res.body.should.have.property('status'); // 檢查屬性
                  res.body.should.have.property('count'); // 檢查屬性
                  done()
              });
      });

## post json .send()
      it('測試 POST /orders/ 回傳json,檢查屬性', function(done) {
          request.post('/orders/')  
              .set('Content-Type', 'application/json') 
              .set('Accept', 'application/json') // 檢查 回傳格式為 JSON
              .send({
                "productID": "5c871485fa1de42134857a2d",
                "quantity": 2
              })
              .expect('Content-Type', /json/) 
              .expect(201) // 檢查  回傳 HTTP 狀態碼為 200
              .end(function(err, res){
                  if (err) return done(err);
                  should.not.exist(err); // 沒有err
                  should.exist(res);  // 有資料
                  res.body.should.be.an('object'); // 內容是物件
    
                  res.body.should.have.property('message'); // 檢查屬性              
                  res.body.should.have.property('createdOrder');            
                  done()
              });
      });

## post files .field() .attach()

      it('測試 POST /products/ 回傳json,檢查屬性', function(done) {
          request.post('/products/')   
              .set('Accept', 'application/json') // 檢查 回傳格式為 JSON
              .type('form')
              .field({
                'name': 'harry',
                'price': 1.99
              })
              .attach('productImage','./test/DSC_0011.jpg')
              .expect('Content-Type', /json/) 
              // .expect('Content-Length', '15') 
              .expect(201) // 檢查  回傳 HTTP 狀態碼為 200
              .end(function(err, res){
                  if (err) return done(err);
                  should.not.exist(err); // 沒有err
                  should.exist(res);  // 有資料
                  res.body.should.be.an('object'); // 內容是物件
    
                  res.body.should.have.property('message'); // 檢查屬性              
                  res.body.should.have.property('createdProduct');           
                  res.body.createdProduct.should.have.property('name');     
                  res.body.createdProduct.should.have.property('price');   
                  res.body.createdProduct.should.have.property('_id');   
                  res.body.createdProduct.should.have.property('request'); 
                  res.body.createdProduct.request.should.have.property('type'); 
                  res.body.createdProduct.request.should.have.property('url'); 
                  done()
              });
      });