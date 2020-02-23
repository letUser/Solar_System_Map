<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Upit",
    props: {},
    data() {
        return {
            x: 0,
            y: 0,
            z: 0,

        };
    },
    methods: {
        takeGEO: function() {
            let upitXYZ = Astronomy.Body[16].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = upitXYZ.x;
            this.y = upitXYZ.y;
            this.z = upitXYZ.z;
        }
    }
    
}
</script>