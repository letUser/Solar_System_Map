<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Nep",
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
            let nepXYZ = Astronomy.Body[19].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = nepXYZ.x;
            this.y = nepXYZ.y;
            this.z = nepXYZ.z;
        }
    }
    
}
</script>