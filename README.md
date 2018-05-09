# 利用CSS变量实现令人震惊的悬停效果

## 怎样才能达到这个效果，使我们的网站脱颖而出呢？其实，它并不像你想象的那么难！

## 追踪位置
    我们要做的第一件事就是获取到鼠标的位置。
### document.querySelector('.button').onmousemove = (e) => {

     const x = e.pageX - e.target.offsetLeft
     const y = e.pageY - e.target.offsetTop

     e.target.style.setProperty('--x', `${ x }px`)
     e.target.style.setProperty('--y', `${ y }px`)

     }

    1、选择元素，等待，直到用户将鼠标移过它；
    2、计算相对于元素的位置；
    3、将坐标存在CSS的变量中。
### 是的，仅仅9行代码就让你能获知用户放置鼠标的位置，通过这个信息你能达到意想不到的效果，但是我们还是先来完成CSS部分的代码。

## 动画渐变
    我们先将坐标存储在CSS变量中，以便能够随时使用它们。

    .button {
      position: relative;
      appearance: none;
      background: #f72359;
      padding: 1em 2em;
      border: none;
      color: white;
      font-size: 1.2em;
      cursor: pointer;
      outline: none;
      overflow: hidden;
      border-radius: 100px;

      span {
        position: relative;
      }

      &::before {
        --size: 0;  

        content: '';
        position: absolute;
        left: var(--x);
        top: var(--y);
        width: var(--size);
        height: var(--size);
        background: radial-gradient(circle closest-side, #4405f7, transparent);
        transform: translate(-50%, -50%);
        transition: width .2s ease, height .2s ease;
      }

      &:hover::before {
        --size: 400px;
      }
    }
    用span包裹文本，以避免显示在按钮的上方。
    将 width和height初始化为0px，当用户悬停在按钮上时，将其改为400px。不要忘了设置这种转换以使其像风一样💨瞬间出现；

## 利用坐标追踪鼠标位置；
    在background 属性上应用 radial-gradient，使用closest-side circle。Closest-side能够覆盖整个面。
## 结果
    成功啦！将其加入到对于的HTML页面，你炫酷的按钮就可以使用啦！
