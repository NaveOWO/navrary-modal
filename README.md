### Navrary-modal

간단한 열고 닫는 기능을 가진 모들 라이브러리입니다.

### 설치방법
```
npm install navrary-modal
```

### 사용법

⚠️ 해당 라이브러리는 `styled-components` & `typescript`를 사용합니다.

1️⃣ Basic

```js
import {Modal} from "navrary-modal"

<Modal defaultOpen>
  <Modal.Backdrop/>
  <Modal.Trigger/>
  <Modal.Contents>
    {children}
  </Modal.Contents>
</Modal>
```

- 모달의 구조는 반드시 `<Modal>`컴포넌트가 최상위 부모가 되어야합니다.
- `<Modal>`컴포넌트 하위에 있는 모든 컴포넌트들은 순서, 위치, 스타일에 구애받지 않고 자유롭게 사용될 수 있습니다.
- 각 컴포넌트들은 children을 받을수도 & 받지 않을수도 있습니다.
- 기본 사용 형태는 위와 같습니다.

2️⃣ Options ( Optional )

```js
function Outside() {
  const [isOpen, setIsOpen[ = usestate(false);
  
  function openModal() {
    setIsOpen(true)
  }
  
  function closeModal() {
    setIsOpen(false)
  }
  
  return (
  <Modal modalState={{isOpen,openModal,closeModal}}>
    {children}
  </Modal>
  )
}
```

- modalState : 모달의 열림 & 닫힘 상태가 모달 컴포넌트 외부와 공유되어야 할 때 해당 상태를 <Modal>컴포넌트에 넣어줄 수 있습니다. <br/>
전달하는 외부상태는 반드시 `{ isOpen : 모달이 열렸는지의 여부, openModal : 모달을 여는 함수, closeModal : 모달을 닫는 함수 }` 형태여아합니다.

```js
function Outside() {
  
  return (
  <Modal defaultOpen>
    {children}
  </Modal>
  )
}
```

- defaultOpen : 모달이 trigger에 의해서가 아닌 자동으로 열리게 설정하고싶을 때 해당 옵션을 <Modal>컴포넌트에 넣어줄 수 있습니다.

- asChild : 컴포넌트의 스타일을 커스텀할 수 있는 옵션입니다. 이 옵션은 반드시 children과 함께 사용되어야 합니다. (3️⃣ 설명 참고)

3️⃣ Custom Style

모든 Modal의 하위 컴포넌트들은 props의 전달 없이 `asChild` 옵션을 통해 모든 스타일 커스텀이 가능합니다. <br/>
(Trigger button의 스타일 커스텀의 예)

```js

function Outside() {
  
  return (
  <Modal >
    <Modal.Trigger asChild>
      <CustomedTrigger/>
    </Modal.Trigger>
  </Modal>
  )
}

const CustomedTrigger = styled.button`
  background-color : "yellow",
`
```

위와같이 `<Modal.Trigger>`의 자식으로 스타일링 된 Trigger을 생성한 뒤, <Modal.Trigger> 컴포넌트에 asChild 속성을 줍니다. <br/>
그렇다면 스탕일링 된 Trigger 컴포넌트는 기존 <Modal.Trigger> 컴폰너트와 똑같은 기능을 수행할 수 있습니다. <br/>
⚠️ 이때 스타일링 된 자식 컴포넌트는 반드시 1개여아합니다.

```js
function Outside() {
  
  return (
  <Modal >
    <Modal.Trigger asChild>
      <YellowTrigger/>
      <RedTrigger/>
    </Modal.Trigger>
  </Modal>
  )
}

const YellowTrigger = styled.button`
  background-color : "yellow",
`

const RedTrigger = styled.button`
  background-color : "red",
`
// ❌ERROR❌

function Outside() {
  
  return (
  <Modal >
    <Modal.Trigger asChild>
      <YellowTrigger>
        <SubStyle/>
      </YellowTrigger>
    </Modal.Trigger>
  </Modal>
  )
}

const YellowTrigger = styled.button`
  background-color : "yellow",
`

const SubStyle = styled.button`
  background-color : "red",
`
//⭕️GOOD⭕️
```








