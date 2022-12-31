<script>
    import { Canvas, Layer } from "svelte-canvas";

    export let size = 1;
    export let width = 256;
    export let height = 256;
    let canvasRef = null;
    $: render = ({ context, width, height }) => {
        for(let i = 0;i < width;i++) {
            for(let j = 0;j < height;j++) {
                context.fillStyle = randomColor();
                context.fillRect(i > 0 ? i * size : i, j > 0 ? j * size : j, size, size);
            }
        }
    };

    const toDataURL = () => {
        canvasRef.getCanvas().toDataURL();
    };
    
    const randomColor = () => {
        return '#'+(Math.random() * 0xFFFFFF << 0).toString(16).padStart(6, '0');
    }
</script>

<Canvas bind:this={canvasRef} width={width} height={height}>
    <Layer {render} />
</Canvas>