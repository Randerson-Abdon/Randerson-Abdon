class x {
    var l = mutableListOf<y>()
    fun a(n: String, e: String): Boolean {
        val a = y(n, e)
        l.forEach {
            if (it.b == a.b) return false
        }
        l.add(a)
        return true
    }
}

data class y(val b: String, val c: String)
