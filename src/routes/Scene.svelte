<script lang="ts">
    import { T, useFrame } from "@threlte/core";
    import { interactivity, OrbitControls, GLTF } from "@threlte/extras";
    import {spring} from "svelte/motion";
    interactivity()

    export let size: {width: number, height: number}
    export let scroll: number
    const boxScale = spring(5)
    let rotation = 0

    useFrame(() => {
        rotation += 0.01
    })
    
</script>


<T.PerspectiveCamera makeDefault 
    args={[75, size.width / size.height, 0.1, 100]} 
    on:create={({ref, cleanup}) => {
        ref.position.setZ(20)
}}>
    <!-- <OrbitControls 
        autoRotate
        enableDamping
        dampingFactor={0.05}
    /> -->
</T.PerspectiveCamera>
<T.AmbientLight color="white" intensity={1}/>
<!-- <T.DirectionalLight 
    
    color="white" 
    intensity={1} 
    position={[0, 10, 10]}
/> -->

<GLTF url="/hyperion/hyperion.glb" 
    rotation={[45 - (scroll * 0.0015), -45, 0]}
    postion={[0, 0, 0]}
    scale={6}
on:create={({ref, cleanup}) => {
}}/>

<!-- <T.Mesh
    scale={$boxScale}
    on:pointerenter={() => boxScale.set(1.25)}
    on:pointerleave={() => boxScale.set(1)}
>
    <T.SphereGeometry args={[3, 64, 64]}/>
    <T.MeshStandardMaterial color="red"/>
</T.Mesh> -->

```