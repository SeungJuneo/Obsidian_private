---
date: 2024-12-19
tages:
  - firebase
---
![[Pasted image 20241219113904.png]]




![[Pasted image 20241219113937.png]]




![[Pasted image 20241219113954.png]]
###### 변수명으로 한글이 가능합니다
```
#데이터 읽고 쓰기
getDocs(collection(db, "product"))

      .then((결과) => {

        결과.forEach((doc) => {

          console.log(doc.id, " => ", doc.data());

          var 템플릿 = `<div class="product">

        <div

          class="thumbnail"

          style="background-image: url('${doc.data().Url}')"

        ></div>

        <div class="flex-grow-1 p-4">

          <h5 class="title">${doc.data().제목}</h5>

          <p class="date">${doc.data().날짜}</p>

          <p class="price">${doc.data().가격}원</p>

          <p class="float-end">?0</p>

        </div>

      </div>`;

          $(".container").append(템플릿);

        });

      })

      .catch((error) => {

        console.log("Error getting documents: ", error);

      });




#데이터 읽기
업로드작업.on(

              "state_changed",

              null,

              (error) => {

                console.error("실패사유는", error);

              },

              () => {

                getDownloadURL(업로드작업.snapshot.ref).then((url) => {

                  console.log("업로드된 경로는", url);

                  const docRef = addDoc(collection(db, "product"), {

                    제목: 제목,

                    가격: parseInt(가격),

                    내용: 내용,

                    위도: 위도,

                    경도: 경도,

                    날짜: new Date().toLocaleDateString(),

                    Url: url,

                  }).then((docRef) => {

                    console.log("문서가 추가되었습니다. 문서 ID:", docRef.id);

                    window.location.href = "/index.html";

                  });

                });

              }

            );
           
#firebase 상에서 회원가입 기능 제공
    const db = getFirestore(app);

    const storage = getStorage(app);

    const auth = getAuth(app);

    $("#register").click(function () {

      const createUser = async (email, password) => {

        try {

          const 유저정보 = await createUserWithEmailAndPassword(

            auth,

            email,

            password

          );

          const 유저 = 유저정보.user;

          console.log("사용자 생성 성공:", 유저);

        } catch (error) {

          if (error.code === "auth/email-already-in-use") {

            window.location.href = "/upload.html";

          } else {

            console.error("사용자 생성 실패:", error.code, error.message);

          }

        }

      };

      var email = $("#email-new").val();

      var password = document.getElementById("pw-new").value;

      createUser(email, password);

    });
```