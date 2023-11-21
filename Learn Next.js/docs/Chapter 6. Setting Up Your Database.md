Chapter 6

# 데이터베이스 설정하기

대시보드 작업을 계속하기 전에 데이터가 필요합니다. 이 장에서는 `@vercel/postgres`를 사용하여 PostgreSQL 데이터베이스를 설정합니다. 이미 PostgreSQL에 익숙하고 자체적으로 데이터베이스를 구축하려는 경우 이 장을 건너뛰고 직접 설정할 수 있습니다. 그렇지 않다면 계속해봅시다!

&nbsp;

> ### 이 장에서는...
>
> 다음과 같은 주제들을 다룰 예정입니다.
>
> - 프로젝트를 GitHub에 푸시합니다.
> - Vercel 계정을 만들고 미리보기와 배포를 위해 GitHub 저장소를 연결합니다.
> - PostgreSQL 데이터베이스를 생성하고 프로젝트와 연결합니다.
> - 초기 데이터로 데이터베이스에 시드를 심습니다.

&nbsp;

---

&nbsp;

## GitHub 저장소 만들기

시작하기위해 아직 리포지토리를 GitHub에 푸시하지 않았다면, 푸시합시다. 이렇게 하면 데이터베이스를 설정하고 배포하는 것이 더 쉬워집니다.

리포지토리 설정에 도움이 필요하면 [GitHub의 가이드](https://help.github.com/en/github/getting-started-with-github/create-a-repo)를 확인하세요.

> **유용한 정보:**
>
> - GitLab 또는 Bitbucket과 같은 다른 Git 제공 업체도 사용할 수 있습니다.
> - GitHub를 처음 사용하는 경우 [GitHub 데스크톱 앱](https://desktop.github.com/)을 사용한 단순화된 개발 워크플로우를 추천합니다.

&nbsp;

---

&nbsp;

## Vercel 계정 만들기

계정을 만들려면 [vercel.com/signup](https://vercel.com/signup)에 방문하세요. 무료 "hobby" 플랜을 선택하세요. GitHub와 Vercel 계정을 연결하려면 **Connect with Github**을 선택하세요.

&nbsp;

---

&nbsp;

## 프로젝트 연결 및 배포

다음 화면으로 이동하게 됩니다. 여기서 방금 만든 GitHub 리포지토리를 선택하고 **가져오기**를 할 수 있습니다:

![Vercel 대시보드 스크린샷, 사용자의 GitHub 리포지토리 목록이 있는 프로젝트 가져오기 화면](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fimport-git-repo.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

프로젝트 이름을 지정하고 배포를 클릭하세요.

![프로젝트 이름 필드와 배포 버튼이 있는 배포 화면](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fconfigure-project.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

만세! 🎉 프로젝트가 이제 배포되었습니다.

![프로젝트 개요 화면, 프로젝트 이름, 도메인 및 배포 상태가 표시됩니다](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fdeployed-project.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

GitHub 리포지토리를 연결함으로써, 변경 사항을 **main** 브랜치에 푸시할 때마다 별도의 설정 없이 Vercel이 자동으로 애플리케이션을 재배포합니다. pull request를 열 때에도 [미리보기](https://vercel.com/docs/deployments/preview-deployments#preview-urls)가 가능하여 배포 오류를 미리 확인하고 프로젝트의 미리보기를 팀원들과 공유할 수 있습니다.

&nbsp;

---

&nbsp;

## PostgreSQL 데이터베이스 만들기

다음으로 데이터베이스를 설정하기 위해 **Continue to Dashboard**을 클릭하고 프로젝트 대시보드에서 **Storage** 탭을 선택합니다. **Connect Store → Create New → Postgres → Continue**를 선택하세요.

![Postgres 옵션과 KV, Blob 및 Edge Config이 표시된 Connect Store 화면](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fcreate-database.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

약관을 수락하고 데이터베이스에 이름을 지정하고 데이터베이스 지역을 **Washington D.C (iad1)**로 설정하세요 - 이는 또한 모든 새로운 Vercel 프로젝트의 [기본 지역](https://vercel.com/docs/functions/serverless-functions/regions#select-a-default-serverless-region)입니다. 데이터베이스를 응용 프로그램 코드와 같은 지역이나 가까운 곳에 배치하면 데이터 요청의 [지연 시간](https://developer.mozilla.org/en-US/docs/Web/Performance/Understanding_latency)을 줄일 수 있습니다.

![데이터베이스 생성 모달, 데이터베이스 이름과 지역이 표시됩니다](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fdatabase-region.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

> **참고**: 데이터베이스 지역은 한 번 설정한 이후로 변경할 수 없습니다. 다른 [지역](https://vercel.com/docs/storage/vercel-postgres/limits#supported-regions)을 사용하려면 데이터베이스를 만들기 전에 설정해야 합니다.

연결하면 `.env.local` 탭으로 이동하여 **Show secret** 및 **Copy Snippet**을 클릭하세요. 복사하기 전에 비밀 키가 노출되는지 확인하세요.

![숨김 처리된 데이터베이스 비밀 키를 보여주는 .env.local 탭](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fdatabase-dashboard.png&w=1920&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

코드 에디터로 이동하여 `.env.example` 파일을 **`.env`**로 이름을 변경하세요. Vercel에서 복사한 내용을 붙여넣으세요.

**중요**: `.gitignore` 파일로 이동하여 `.env`가 무시되도록 하여 GitHub에 푸시할 때 데이터베이스 비밀 키가 노출되지 않도록 해야 합니다.

마지막으로 터미널에서 `npm i @vercel/postgres`를 실행하여 [Vercel Postgres SDK](https://vercel.com/docs/storage/vercel-postgres/sdk)를 설치하세요.

&nbsp;

---

&nbsp;

## 데이터베이스 시드 작성하기

이제 데이터베이스를 생성했으니 초기 데이터로 시드를 심어봅시다. 대시보드를 구축하는 동안 사용할 데이터를 가져오게 됩니다.

프로젝트의 `/scripts` 폴더에 `seed.js`라는 파일이 있습니다. 이 스크립트에는 `invoices`, `customers`, `user`, `revenue` 테이블을 생성하고 시드를 심는 지침이 포함되어 있습니다.

코드가 하는 일을 완전히 이해하지 못하더라도 걱정하지 마세요. 이 스크립트는 **SQL**을 사용하여 테이블을 생성하고, 생성된 후에 `placeholder-data.js` 파일의 데이터를 사용하여 테이블에 데이터를 채웁니다.

그 다음으로, `package.json` 파일에 다음 라인을 스크립트에 추가하세요:

`/package.json`

```json
"scripts": {
  "build": "next build",
  "dev": "next dev",
  "start": "next start",
  "seed": "node -r dotenv/config ./scripts/seed.js"
},
```

이 명령은 `seed.js`를 실행할 것입니다.

이제 `npm run seed`를 실행하세요. 터미널에서 일부 `console.log` 메시지를 볼 수 있어야 스크립트가 실행되고 있다는 것을 알 수 있을 것입니다.

&nbsp;

> ### 퀴즈 시간입니다!
>
> 지식을 테스트하고 방금 배운 내용을 확인하세요.
>
> **데이터베이스에서 '시딩(seeding)'은 무엇을 의미하나요?**
>
> -A: 데이터베이스의 모든 데이터 삭제
> -B: 데이터베이스의 스키마 가져오기
> -C: 데이터베이스에 초기 데이터 집합 채우기
> -D: 데이터베이스의 테이블 간 관계 생성
>
> &nbsp;
>
> #### 정답 확인
>
> **C: 데이터베이스에 초기 데이터 집합 채우기**

&nbsp;

> **문제 해결:**
>
> - `.env` 파일로 복사하기 전에 데이터베이스 비밀 키를 표시했는지 확인하세요.
> - 스크립트는 사용자의 비밀번호를 해싱하기 위해 `bcrypt`를 사용합니다. `bcrypt`가 환경과 호환되지 않는 경우 스크립트를 [`bcryptjs`](https://www.npmjs.com/package/bcryptjs)로 업데이트할 수 있습니다.
> - 데이터베이스 시드 중에 문제가 발생해서 스크립트를 다시 실행하고 싶다면 데이터베이스 쿼리 인터페이스에서 `DROP TABLE tablename`을 실행하여 기존 테이블을 삭제할 수 있습니다. 자세한 내용은 [쿼리 실행 섹션](https://nextjs.org/learn/dashboard-app/setting-up-your-database#executing-queries)을 참조하세요. 하지만 조심하세요, 이 명령은 테이블과 해당 데이터를 모두 삭제합니다. 예제 앱에서는 플레이스홀더 데이터를 사용하기 때문에 이 명령을 실행해도 상관없지만, 프로덕션 앱에서는 이 명령을 실행하지 않아야 합니다.
> - Vercel Postgres 데이터베이스 시딩 중에 계속 문제가 발생하는 경우 [GitHub Discussion](https://github.com/vercel/next-learn/issues)을 열어주세요.

&nbsp;

---

&nbsp;

## 데이터베이스 탐색

데이터베이스를 확인해봅시다. Vercel로 돌아가서 사이드 네비게이션에서 **Data**를 클릭하세요.

이 섹션에서는 새로 생성된 네 가지 테이블을 찾을 수 있습니다: users, customers, invoices, revenue.

![네 가지 테이블(users, customers, invoices, revenue)이 드롭다운 목록으로 표시된 데이터베이스 화면](https://nextjs.org/_next/image?url=%2Flearn%2Flight%2Fdatabase-tables.png&w=2048&q=75&dpl=dpl_H7MBMnAb8vFgYfWdWcJLkssQPv5e)

각 테이블을 선택하여 해당 레코드를 확인하고 `placeholder-data.js` 파일의 데이터와 일치하는지 확인할 수 있습니다.

&nbsp;

---

&nbsp;

## 쿼리 실행

"쿼리" 탭으로 전환하여 데이터베이스와 상호작용할 수 있습니다. 이 섹션은 표준 SQL 명령을 지원합니다. 예를 들어 `DROP TABLE customers`를 입력하면 "customers" 테이블과 해당 데이터를 모두 삭제합니다. **_- 그러니 조심하세요_**!

첫 번째 데이터베이스 쿼리를 실행해봅시다. 아래 SQL 코드를 Vercel 인터페이스에 붙여넣고 실행해보세요:

```sql
SELECT invoices.amount, customers.name
FROM invoices
JOIN customers ON invoices.customer_id = customers.id
WHERE invoices.amount = 666;
```

&nbsp;

> ### 퀴즈를 풀어보세요!
>
> 지금까지 배운 내용을 확인해보세요.
>
> **이 인보이스는 어떤 고객에게 속해 있나요?**
>
> -A: Lee Robinson
> -B: Evil Rabbit
> -C: Delba de Oliveira
> -D: Steph Dietz
>
> &nbsp;
>
> #### 정답 확인
>
> **B: Evil Rabbit**
