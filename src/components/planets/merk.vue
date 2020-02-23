<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Merk",
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
            let merkXYZ = Astronomy.Body[1].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = merkXYZ.x;
            this.y = merkXYZ.y;
            this.z = merkXYZ.z;
        }
    }
    
}
</script>