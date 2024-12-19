---
date: 2024-12-19
tages:
  - firebase
---
![[Pasted image 20241219113904.png]]




![[Pasted image 20241219113937.png]]




![[Pasted image 20241219113954.png]]
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




#읽기






























```