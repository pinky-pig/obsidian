1.  https://playground.mmeme.me/
文档总结，以及 bug 修改

bug 复现，将下面 html 代码拷贝进去就行了

```html
<!DOCTYPE html>
<html>
<head>
  <title>Parabolic Curve</title>
</head>
<body>
  <canvas id="parabolicCanvas" width="300" height="200"></canvas>

  <script>
    const canvas = document.getElementById('parabolicCanvas');
    const ctx = canvas.getContext('2d');

    // 给定两点坐标
    const startPoint = [0, 100];
    const endPoint = [100, 50];

    // 控制点坐标（中点）
    const controlPoint = [(startPoint[0] + endPoint[0]) / 2, Math.min(startPoint[1], endPoint[1]) - 100];

    ctx.beginPath();
    ctx.moveTo(startPoint[0], startPoint[1]);
    ctx.quadraticCurveTo(controlPoint[0], controlPoint[1], endPoint[0], endPoint[1]);

    ctx.lineWidth = 2;
    ctx.strokeStyle = 'blue';
    ctx.stroke();

  </script>
</body>
</html>

```