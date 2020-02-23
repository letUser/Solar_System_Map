<script>
import { Astronomy } from "./calculations/astronomy.js";

export default {
    name: "Ur",
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
            let urXYZ = Astronomy.Body[18].EclipticCartesianCoordinates(Astronomy.DayValue(new Date()));

            this.x = urXYZ.x;
            this.y = urXYZ.y;
            this.z = urXYZ.z;
        }
    }
    
}
</script>