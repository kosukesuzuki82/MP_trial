# MP_trial
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <link rel="stylesheet" href="css/reset.css">
  <link rel="stylesheet" href="css/login.css">
  <title>Metal Place</title>
</head>

<!-- 登録なしポップアップ -->
<form class="form_regi" name="login_form" hidden >
  <div class="login_form_top">
    <h1>登録がありません</h1>
    <a href="MP_user_regi.html">初めての方はこちら</a>
  </div>
  <div class="login_form_btm">
    <button class="close">閉じる</button>
  </div>
</form>

<body>
  <!-- ログイン/画面 -->
  <section class="login">
    <form name="login_form">
      <div class="login_form_top">
        <h1>ログイン</h1>
        <p>ID、Passwordをご入力の上、「LOGIN」ボタンをクリックしてください。</p>
      </div>
      <div class="login_form_btm">
        <input type="id" name="user_id" placeholder="ID" class="u_id">
        <input type="password" name="password" placeholder="Password" class="u_pass">
        <input type="button" name="button" value="LOGIN" class="login_button">
      </div>
      <a href="MP_user_regi.html">初めての方はこちら</a>
    </form>
  </section>

<!-- Firedatabaseインストール -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.js"></script>
  <script type="module">
    // Import the functions you need from the SDKs you need
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
    // TODO: Add SDKs for Firebase products that you want to use
    // https://firebase.google.com/docs/web/setup#available-libraries
    import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut }
      from "https://cdnjs.cloudflare.com/ajax/libs/firebase/9.15.0/firebase-auth.js" 
    import { getDatabase, ref, push, set, onChildAdded, remove, onChildRemoved }
        from "https://cdnjs.cloudflare.com/ajax/libs/firebase/9.15.0/firebase-database.js";
  
    // Your web app's Firebase configuration
    const firebaseConfig = {
      apiKey: "AIzaSyBohcWZ_eAC_E1RcM1UfIWvLO_5yUTvsL4",
      authDomain: "metal-trial.firebaseapp.com",
      databaseURL: "https://metal-trial-default-rtdb.firebaseio.com",
      projectId: "metal-trial",
      storageBucket: "metal-trial.appspot.com",
      messagingSenderId: "111277777807",
      appId: "1:111277777807:web:c0cd1d622675d873e161fa"
    };
  
    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);//Real Time DBに接続
    const dbRef = ref(db, "register");//Realtime DB内のチャットを使う指示

  //registerに登録があるユーザー名だったら、ページ遷移/なければ登録なしと出る→未登録
  $(".login_button").on("click",function(){
    const id_log = $(".u_id").val();
    const pass_log = $(".u_pass").val();
    onChildAdded(dbRef,function(data){
      const msg = data.val();
      //取得したデータに一致するデータがあるかをデータの数繰り返す/判定する
      //登録があるコードを取得する
      const id_reg = (msg["id"]);
      const pass_reg = (msg["pass"]);
      console.log(id_reg,pass_reg);
      if(id_reg==id_log && pass_reg==pass_log){
        window.location.href = "MP_material_register.html";
      }
      else{
        console.log("一致無し");
      }  
    })
    //登録がなかった場合の表示
  })

  
</script>

  
</body>
