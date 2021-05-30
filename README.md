# node-recaptcha
valida formulário no request client

#script paraa colocar no head

```
 <script src="https://www.google.com/recaptcha/api.js" async defer></script>
```

#Fomulário de Teste

```
    <div class="container"><br />
        <h1>Validação de formulario com Recaptcha v2</h1><br />

        <form action="/captcha" method="POST">
            <div class="g-recaptcha" data-sitekey={{site_key}}></div>
                <br/>
            <input type="submit" value="Submit">
         </form>

    </div>
```

#codigo que request recebe no link de Post

```
 if(req.body['g-recaptcha-response'] === undefined || req.body['g-recaptcha-response'] === '' || req.body['g-recaptcha-response'] === null)
  {
    console.log(req.body)
    return res.json({"responseError" : req.body});
  }
  const secretKey = process.env.SECRET_KEY;

  const verificationURL = "https://www.google.com/recaptcha/api/siteverify?secret=" + secretKey + "&response=" + req.body['g-recaptcha-response'] + "&remoteip=" + req.connection.remoteAddress;

  request(verificationURL,function(error,response,body) {
    body = JSON.parse(body);

    if(body.success !== undefined && !body.success) {
      return res.json({"responseError" : "Failed captcha verification"});
    }
    res.json({"responseSuccess" : "Sucess"});
  }); 
  ```

  Executa server
  >npm start
